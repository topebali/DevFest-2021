# Introduction
In this guide, You will create two different batch changes:

- A batch change that appends text to `README.md` files in all of your repositories.

- A batch change that finds and replace texts in a set of python files.

## Requirements
- A Sourcegraph instance with some repositories in it. See “[Quick install](https://docs.sourcegraph.com/#quick-install)” on how to set up a Sourcegraph instance.

- A local environment matching [“Requirements”](https://docs.sourcegraph.com/batch_changes/references/requirements) to create batch changes with the Sourcegraph CLI.

## Install the Sourcegraph CLI
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

## Write a Batch Spec
A **batch spec** is a YAML file that defines a batch change. It specifies which changes should be made in which repositories.

### Hands-On Practice One (1)

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

### Hands-On Practice Two (2)

Save the batch spec as `find_and_replace.batch.yaml`:

``` 
name: number-employee_details-wording
description: This batch change updates our Python scripts to use the terms "num1" and "staff_details" instead of "number" and "employee_details".

# Search for repositories in which the term "number" or "employee_details" appears
# in python files.
on:
  - repository: github.com/topebali/test_wordreplace

# In each repository
steps:
  # find all *.py and replace the terms in them:
  - run: |
      find . -type f \( -name '*.py' \) |\
      xargs sed -i 's/number/num1/g; s/employee_details/staff_details/g'       
    container: alpine:3

# Describe the changeset (e.g., GitHub pull request) you want for each repository.
changesetTemplate:
  title: Replace number/employee_details with num1/staff_details
  body: This replaces the terms number/employee_details in Python files with num1/staff_details
  branch: batch-changes/number-employee_details-wording # Push the commit to this branch.
  commit:
    message: Replaces number/employee_details  with num1/staff_details
  published: false
```



## Create the batch change
1. In your terminal, run this command:
`src batch preview -f devfest.batch.yaml`

> For the second hands-on practice change the name to `find_and_replace.batch.yaml`

2. Wait for it to run and compute the changes for each repository.

3. When it’s done, follow the link to the preview page to see all the changes that will be made.

4. Make sure the changes look right.

5. Click **Apply** to create the batch change.

**You’ve now created your first batch change!

For more information on Batch change visit our Batch changes [page](https://docs.sourcegraph.com/batch_changes/quickstart) in our Documentation.