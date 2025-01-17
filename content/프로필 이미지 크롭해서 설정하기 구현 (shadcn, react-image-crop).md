지
---
title: 프로필 이미지 크롭해서 설정하기 구현 (shadcn, react-image-crop)
date: 2025-01-16
tags:
  - seed
---

참고:

https://github.com/sekoyo/react-image-crop

https://github.com/sujjeee/shadcn-image-cropper/blob/main/src/components/image-cropper.tsx

추가 구현:

```tsx
'use client';

import 'react-image-crop/dist/ReactCrop.css';

import { CropIcon } from 'lucide-react';
import React, { type SyntheticEvent, useState } from 'react';
import { FileWithPath, useDropzone } from 'react-dropzone';
import ReactCrop, {
  centerCrop,
  type Crop,
  makeAspectCrop,
  type PixelCrop,
} from 'react-image-crop';
import { toast } from 'sonner';

import { cn, base64ToFile } from '~/lib/utils';
import { Avatar, AvatarFallback, AvatarImage } from '~/ui/avatar';
import { Button } from '~/ui/button';
import {
  Dialog,
  DialogClose,
  DialogContent,
  DialogDescription,
  DialogFooter,
  DialogHeader,
  DialogTitle,
} from '~/ui/dialog';
import LoadingIcon from '~/ui/icons';

export type FileWithPreview = FileWithPath & {
  preview: string;
};

interface ImageCropperProps {
  aspect?: number;
  className?: string;
  disabled?: boolean;
  id?: string;
  name?: string;
  defaultImage?: string;
  onChange?: (file: File) => void;
}

export function ImageCropper({
  id,
  name,
  defaultImage,
  aspect = 1,
  className,
  onChange,
}: ImageCropperProps) {
  const imgRef = React.useRef<HTMLImageElement | null>(null);

  const [file, setFile] = useState<FileWithPreview | null>(null);

  const [isDialogOpen, setIsDialogOpen] = useState(false);

  const [crop, setCrop] = useState<Crop>();
  const [croppedImageUrl, setCroppedImageUrl] = useState<string>('');
  const [croppedImage, setCroppedImage] = useState<string>('');

  const { getRootProps, getInputProps } = useDropzone({
    maxFiles: 1,
    onDrop: (acceptedFiles, rejectedFiles) => {
      if (rejectedFiles.length > 0) {
        rejectedFiles.forEach(({ file }) => {
          toast.error(`${file.name} 파일이 유효하지 않습니다.`);
        });
      }

      if (acceptedFiles.length < 1) {
        toast.error('유효한 파일이 없습니다.', {
          description: '유효한 이미지 파일을 선택해주세요.',
        });
        return;
      }

      const file = acceptedFiles[0];

      const fileWithPreview = Object.assign(file, {
        preview: URL.createObjectURL(file),
      });

      setFile(fileWithPreview);
      setIsDialogOpen(true);
    },
    accept: {
      'image/*': [],
    },
  });

  function onImageLoad(e: SyntheticEvent<HTMLImageElement>) {
    if (!aspect) {
      return;
    }

    const { width, height } = e.currentTarget;
    setCrop(centerAspectCrop(width, height, aspect));
  }

  function onCropComplete(crop: PixelCrop) {
    if (imgRef.current && crop.width && crop.height) {
      const croppedImageUrl = getCroppedImg(imgRef.current, crop);
      setCroppedImageUrl(croppedImageUrl);
    }
  }

  function getCroppedImg(image: HTMLImageElement, crop: PixelCrop): string {
    const canvas = document.createElement('canvas');
    const scaleX = image.naturalWidth / image.width;
    const scaleY = image.naturalHeight / image.height;

    canvas.width = crop.width * scaleX;
    canvas.height = crop.height * scaleY;

    const ctx = canvas.getContext('2d');

    if (ctx) {
      ctx.imageSmoothingEnabled = false;

      ctx.drawImage(
        image,
        crop.x * scaleX,
        crop.y * scaleY,
        crop.width * scaleX,
        crop.height * scaleY,
        0,
        0,
        crop.width * scaleX,
        crop.height * scaleY,
      );
    }

    return canvas.toDataURL('image/png', 1.0);
  }

  async function applyCrop() {
    try {
      setCroppedImage(croppedImageUrl);

      const croppedFile = await base64ToFile(croppedImageUrl, 'cropped.png');
      onChange?.(croppedFile);

      setIsDialogOpen(false);
    } catch (e) {
      console.error(e);
      alert('Something went wrong!');
    }
  }

  return (
    <Dialog open={isDialogOpen} onOpenChange={setIsDialogOpen}>
      <button
        {...getRootProps()}
        type="button"
        className={cn(
          'relative size-16 overflow-hidden rounded-full border outline-none',
          'focus:ring-2 focus:ring-border focus:ring-offset-2',
          'transition hover:opacity-80',
          className,
        )}
      >
        <input id={id} name={name} {...getInputProps()} />
        <Avatar className="h-full w-full">
          <AvatarImage src={croppedImage || defaultImage} alt="avatar" />
          <AvatarFallback />
        </Avatar>
      </button>
      <DialogContent>
        <DialogHeader>
          <DialogTitle>이미지 자르기</DialogTitle>
          <DialogDescription>
            이미지에 드래그해서 원하는 부분을 자르세요.
          </DialogDescription>
        </DialogHeader>
        <div className="size-full max-h-[500px] overflow-x-hidden overflow-y-scroll">
          <ReactCrop
            crop={crop}
            onChange={(_, percentCrop) => setCrop(percentCrop)}
            onComplete={(c) => onCropComplete(c)}
            aspect={aspect}
            className="w-full"
          >
            <Avatar className="size-full rounded-none">
              <AvatarImage
                ref={imgRef}
                className="aspect-auto size-full rounded-none object-contain"
                alt="Image Cropper Shell"
                src={file?.preview}
                onLoad={onImageLoad}
              />
              <AvatarFallback className="size-full min-h-[300px] rounded-none">
                <LoadingIcon />
              </AvatarFallback>
            </Avatar>
          </ReactCrop>
        </div>
        <DialogFooter>
          <DialogClose asChild>
            <Button
              type="reset"
              variant={'outline'}
              onClick={() => {
                setFile(null);
              }}
            >
              닫기
            </Button>
          </DialogClose>
          <Button type="submit" onClick={applyCrop}>
            <CropIcon className="size-4" />
            자르기
          </Button>
        </DialogFooter>
      </DialogContent>
    </Dialog>
  );
}

export function centerAspectCrop(
  mediaWidth: number,
  mediaHeight: number,
  aspect: number,
): Crop {
  return centerCrop(
    makeAspectCrop(
      {
        unit: '%',
        width: 50,
        height: 50,
      },
      aspect,
      mediaWidth,
      mediaHeight,
    ),
    mediaWidth,
    mediaHeight,
  );
}
```