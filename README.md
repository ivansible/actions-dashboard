## Github Actions Dashboard

This tool generates a dashboard that shows live status of all github action
workflows in a given set of github repositories.

The [`generate.sh`](./generate.sh) script can read input files that contain
single line records of github repositories, scan all workflows listed in
`.github/workflows` and generate a markdown file that shows the current status
of each workflow.

### Usage
```sh
generate.sh [-h] -o OUTFILE [-i FILE]...

    -h  display this help
    -i  input file path
    -o  output markdown file path
```

You can provide multiple input files. The input file value can be a local file
path or an http(s) url.

Input files must have a github repository name per line that follows the syntax
`<user-or-org>/<repo>`.

Lines beginning with `#` are treated as comments.

E.g.
```sh
./generate.sh -o dashboard.md -i repos.txt \
  -i https://raw.githubusercontent.com/arjun024/actions-dashboard/master/samples/some-other-gcp-repos
```

See [sample input](./repos.txt) and [sample output](./dashboard.md).

<img src="https://github.com/ivansible/actions-dashboard/blob/master/sample.png?raw=true" width="550">


### Auto-regenerate

You can use a [github workflow like
this](.github/workflows/update-dashboard.yml) that runs the generate script
every day to see if any workflow files have been added/removed from the repos
listed in the input files.

### How to use

* Fork this repository
* Edit the sample input to list your repositories or create an input file or
  point to to your list of repos elsewhere
* Run the generate script with the required options
* Edit
  [`.github/workflows/update-dashboard.yml`](.github/workflows/update-dashboard.yml)
  to run `generate.sh` with your command options in the `Generate` step.

