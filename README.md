<h1 align="center">Potential Duplicates</h1>

<p align="center">
  <a href="https://github.com/iv-org/close-potential-duplicates/actions/workflows/release.yml"><img alt="build" src="https://img.shields.io/github/actions/workflow/status/iv-org/close-potential-duplicates/release.yml?branch=master&logo=github&style=flat-square" ></a>
  <a href="/iv-org/close-potential-duplicates/blob/master/LICENSE"><img alt="MIT License" src="https://img.shields.io/github/license/iv-org/close-potential-duplicates?style=flat-square"></a>
  <a href="https://www.typescriptlang.org" rel="nofollow"><img alt="Language" src="https://img.shields.io/badge/language-TypeScript-blue.svg?style=flat-square"></a>
  <a href="https://github.com/iv-org/close-potential-duplicates/pulls"><img alt="PRs Welcome" src="https://img.shields.io/badge/PRs-Welcome-brightgreen.svg?style=flat-square" ></a>
  <a href="https://github.com/marketplace/actions/close-potential-duplicates" rel="nofollow"><img alt="website" src="https://img.shields.io/static/v1?label=&labelColor=505050&message=Marketplace&color=0076D6&style=flat-square&logo=google-chrome&logoColor=0076D6" ></a>
  <a href="https://lgtm.com/projects/g/iv-org/close-potential-duplicates/context:javascript" rel="nofollow"><img alt="Language grade: JavaScript" src="https://img.shields.io/lgtm/grade/javascript/g/iv-org/close-potential-duplicates.svg?logo=lgtm&style=flat-square" ></a>
</p>

<p align="center">
  <strong>
    Search for potential issue duplicates using <a href="https://en.wikipedia.org/wiki/Damerau%E2%80%93Levenshtein_distance">Damerau–Levenshtein</a> algorithm and close it.
  </strong>
</p>

## Usage

Create `.github/workflows/close-potential-duplicates.yml` in the default branch:

```yaml
name: Potential Duplicates
on:
  issues:
    types: [opened, edited]
jobs:
  run:
    runs-on: ubuntu-latest
    steps:
      - uses: iv-org/close-potential-duplicates@v1
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          # Issue title filter work with anymatch https://www.npmjs.com/package/anymatch.
          # Any matched issue will stop detection immediately.
          # You can specify multi filters in each line.
          filter: ''
          # Exclude keywords in title before detecting.
          exclude: ''
          # Label to set, when potential duplicates are detected.
          label: potential-duplicate
          # Get issues with state to compare. Supported state: 'all', 'closed', 'open'.
          state: all
          # If similarity is higher than this threshold([0,1]), issue will be marked as duplicate.
          threshold: 0.6
          # Reactions to be add to comment when potential duplicates are detected.
          # Available reactions: "-1", "+1", "confused", "laugh", "heart", "hooray", "rocket", "eyes"
          reactions: 'eyes, confused'
          # Close or not the issue: false or true
          close: 'false'
          # Comment to post when potential duplicates are detected.
          comment: >
            Potential duplicates: {{#issues}}
              - [#{{ number }}] {{ title }} ({{ accuracy }}%)
            {{/issues}}
```

### Inputs

Various inputs are defined to let you configure the action:

> Note: [Workflow command and parameter names are not case-sensitive](https://docs.github.com/en/free-pro-team@latest/actions/reference/workflow-commands-for-github-actions#about-workflow-commands).

| Name | Description | Default |
| --- | --- | --- |
| `GITHUB_TOKEN` | The GitHub token for authentication | N/A |
| `filter` | Issue title filter work with [anymatch](https://www.npmjs.com/package/anymatch) <br> Any matched issue will stop detection immediately <br> You can specify multi filters in each line | `''` |
| `exclude` | Exclude keywords in title before detecting | `''` |
| `label` | Label to set, when potential duplicates are detected | `'potential-duplicate'` |
| `state` | Get issues with state to compare. Supported state: `'all'` `'closed'` `'open'` | `'all'` |
| `threshold` | If similarity is higher than this threshold(`[0,1]`), issue will be marked as duplicate | `0.6` |
| `reactions` | Reactions to be add to comment when potential duplicates are detected <br> Available reactions: "-1", "+1", "confused", "laugh", "heart", "hooray", "rocket", "eyes" |  |
| `comment` | Comment to post when potential duplicates are detected | 👇 |
| `close` | Close or not the issue when found to be duplicate. | false |

Available reactions:

| content    | emoji |
| ---------- | ----- |
| `+1`       | 👍    |
| `-1`       | 👎    |
| `laugh`    | 😄    |
| `confused` | 😕    |
| `heart`    | ❤️    |
| `hooray`   | 🎉    |
| `rocket`   | 🚀    |
| `eyes`     | 👀    |

Default comment:

```
Potential duplicates: {{#issues}}
  - [#{{ number }}] {{ title }} ({{ accuracy }}%)
{{/issues}}
```

## License

The scripts and documentation in this project are released under the [MIT License](LICENSE)
