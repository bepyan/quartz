---
title: action에서 github 댓글을 편하게 다루기
date: 2024-07-26
tags:
  - seed
  - snippet
---
https://github.com/peter-evans/create-or-update-comment

```
      - name: Create comment
        uses: peter-evans/create-or-update-comment@v4
        with:
          issue-number: 1
          body: |
            This is a multi-line test comment
            - With GitHub **Markdown** :sparkles:
            - Created by [create-or-update-comment][1]

            [1]: https://github.com/peter-evans/create-or-update-comment
          reactions: '+1'

```

```
      - name: Find Comment
        uses: peter-evans/find-comment@v2
        id: fc
        with:
          issue-number: ${{ github.event.pull_request.number }}
          comment-author: "github-actions[bot]"
          body-includes: Preview deployed to
      - name: Create or Update Comment
        uses: peter-evans/create-or-update-comment@v4
        with:
          comment-id: ${{ steps.fc.outputs.comment-id }}
          issue-number: ${{ github.event.pull_request.number }}
          body: |
            Preview deployed to: ${{ steps.deploy.outputs.url }}
            Last updated: ${{ github.event.pull_request.updated_at }}
```
