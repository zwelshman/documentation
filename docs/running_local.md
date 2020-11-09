## Using `cohortextractor` at the command line

The repo contains a working Study Definition (`study_definition.py`) which is used to retreive codelists and create dummy data. Before making any changes to `study_definition.py` to match your study (which will need to be properly version controlled in git), it's important to understand how the study definition is used by `cohortextractor`. Without `cohortextractor` you won't be able to run and test any changes that you've made to `study_definition.py` or the codelists.

To run any of these commands for your specific local repository, you need to change the directory of your prompt to be the repo directory using for example `cd c:/my-repos-folder/my-repo`. To confirm you can use `cohortextractor`, go to a terminal and submit `cohortextractor --help`, which will list all the ways in which you can use it. You can also use `cohortextractor generate_cohort --help` to learn more about the `generate_cohort` command, for example. Some of these commands are discussed in detail below.

#### `generate_cohort`
This will create a dummy dataset for you, `outputs/input.csv`, based on the _expectations_ declared in the study definition. Use it for example like this:

    cohortextractor generate_cohort --expectations-population 10000

where `10000` is the number of rows you want to generate for your dataset.

Run it &mdash; check that `outputs/input.csv` has been created. Run it again -- the file will be refreshed (check the file's _modified_ date) and will contain different data than previously (even if the `study_definition.py` didn't change) because the values are randomly generated.

Beware that on Windows, you can't have `input.csv` open and generate a new one at the same time.

If you have multiple study definitions in the repo (eg `study_definition_set1.py`, `study_definition_set2.py`) then `generate_cohort` will create dataset for each (eg `input_set1.csv`, `intput_set2.csv`). You can restrict it to a single study definition using the `study-definition` option, like this:

    cohortextractor generate_cohort --expectations-population 10000 --study-definition study_definition_set2

This is most useful when extracting real data on the server when only some study definitions have been updated, due to the time taken to run each study definition.


#### `update_codelists`
This will retrieve the codelists from [codelists.opensafely.org](https://codelists.opensafely.org) based on those listed in `/codelists/codelists.txt` and put them in the same folder. Use it like this:

    cohortextractor update_codelists

Run it &mdash; it will add (or update) the codelist `.csv` files in the `codelists/` folder. See [here](https://github.com/opensafely/documentation/blob/master/study_definition.md#codelist-definitions) for more information about how to create codelists.

Beware again that in Windows, if one or more of these codelist files is open then `update_codelists` won't be able to run.


#### `cohort_report`

This will produce an `.html` document giving some summary statistics about each variable in the study dataset. Use it like this:

    cohortextractor cohort_report

Re-run it each time you want to update the document using the latest version of the `input.csv` dataset. Assuming that your working directory is the repo folder, you should be able to run `cohortextractor` commands.
This command can also be run on the real data. For information on this, see the [Running on server](job_server.md) page for further details.