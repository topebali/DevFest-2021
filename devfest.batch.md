# Introduction
In this guide, you’ll create a Sourcegraph batch change that appends text to `README.md` files in all of your repositories.

## Requirements
- A Sourcegraph instance with some repositories in it. See “[Quick install](https://docs.sourcegraph.com/#quick-install)” on how to set up a Sourcegraph instance.

- A local environment matching [“Requirements”](https://docs.sourcegraph.com/batch_changes/references/requirements) to create batch changes with the Sourcegraph CLI.

### Install the Sourcegraph CLI
In order to create batch changes we need to [install the Sourcegraph CLI](https://docs.sourcegraph.com/cli) (`src`).

1. Install the version of src that’s compatible with your Sourcegraph instance:

**macOS**:
```
curl -L https://YOUR-SOURCEGRAPH-INSTANCE/.api/src-cli/src_darwin_amd64 -o /usr/local/bin/src
chmod +x /usr/local/bin/src
```
**Linux**:
```
curl -L https://YOUR-SOURCEGRAPH-INSTANCE/.api/src-cli/src_linux_amd64 -o /usr/local/bin/src
chmod +x /usr/local/bin/src
```
2. Authenticate `src` with your Sourcegraph instance by running `src login` and following the instructions:

```src login https://YOUR-SOURCEGRAPH-INSTANCE```

Once `src login` reports that you’re authenticated, we’re ready for the next step.

### Write a Batch Spec
A **batch spec** is a YAML file that defines a batch change. It specifies which changes should be made in which repositories.

Save the batch spec as `devfest.batch.yaml`:

``` 
name: hello-devfest
description: Add Welcome to devFest to READMEs

# Find all repositories that contain a README.md file.
on:
  - repository: github.com/topebali/test_batch

# In each repository, run this command. Each repository's resulting diff is captured.
steps:
  - run: echo Welcome to devFest | tee -a $(find -name README.md)
    container: alpine:3

# Describe the changeset (e.g., GitHub pull request) you want for each repository.
changesetTemplate:
  title: Welcome to devFest
  body: My first batch change!
  branch: devFest-2021 # Push the commit to this branch.
  commit:
    message: Append Welcome to devFest to all README.md files
```


## Create the batch change
1. In your terminal, run this command:
`src batch preview -f devfest.batch.yaml`

2. Wait for it to run and compute the changes for each repository.

3. When it’s done, follow the link to the preview page to see all the changes that will be made.

4. Make sure the changes look right.

5. Click **Apply** to create the batch change.

**You’ve now created your first batch change!**

For more information on Batch change visit our Batch changes [page](https://docs.sourcegraph.com/batch_changes/quickstart) in our Documentation.