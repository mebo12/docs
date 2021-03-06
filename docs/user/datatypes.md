# Datatypes

> Please read [Tutorial / Datatypes](/docs/user/tutorial/#datatypes) first.

Brainlife Apps exchange data through `datatypes`.

![resources](/docs/img/datatypes.png)

Each datatype consists of `name`, `description`, and a list of files (or directories) that define the overall structure of the datatype. 

For example, the following is a datatype definition for `neuro/life` datatype.

```json
{
    "name" : "neuro/life",
    "desc" : "LiFE Output (fe structure)",
    "files" : [ 
        {
            "id" : "fe",
            "filename" : "output_fe.mat",
            "desc" : "FE structure",
            "ext" : ".mat",
            "required" : true
        }, 
        {
            "id" : "life_results",
            "filename" : "life_results.json",
            "required" : true
        }, 
        {
            "id" : "tracts",
            "dirname" : "tracts",
            "required" : true
        }
    ]
}
```

For this example datatype, `brain-life/app-life` App generates a dataset with this datatype, and other Apps that want to use `neuro/life` output can request to have those files made available to their Apps by registering them on Brainlife App registration form. (Please read [Registering App](/docs/apps/register/) page for more info). The actual content/semantics of each file are up to developers exchanging the dataset to decide, and it should be well documented as part of the datatype registration process.

Please see other datatypes defined in [brainlife/datatypes](https://brainlife.io/datatypes).

Brainlife datatype might sound similar to BIDS specification, but it differs in following areas.

* Brainlife datatypes mainly concern data derivatives generated by Apps and used only by Apps exchanging those datasets. They are only used within Brainlife platform and not meant to become standards for that particular data format.

* Brainlife datatypes are defined by App developers involved in exchanging input/output datasets, not by Brainlife platform developers. App developers should discuss and agree on the structure of the datatype and what each file means (on #datatype channel on brainlife slack). Once Brainlife team incorporate the PR, you will be able to use the new datatype for your App.

## Datatype Tags

Sometimes you want to be more specific about the type of dataset for a particular datatype. For example, `neuro/anat/t1w` could be ACPC aligned or not, `neuro/dwi` could be single-shell or multi-shell, etc. Brainlife allows you to adds specificity to each datatype through *datatype tags*. 

!!! warning
    Please don't confuse *Datatype tag* with *Dataset tag*. "Dataset tag" is a tag that user can freely edit under dataset dialog to allow for easier searching or bulk processing of datasets with specific tags. "Datatype tag", on the other hand, can only be set by App developer and it is a part of datatype and can not be modified once dataset is created.

It is important to note that, *datatype tag* should always be used to add specificity to datasets, but not to generalize it. For example, we don't have "multi-shell" datatype tags because `neuro/dwi` is by default a "multi-shell" data; it is perfectly valid to have different b-values in `dwi.bvals` file. "single-shell" is a special case for `neuro/dwi` datatype where b-values happens to be all same number. Therefore, we introduce "single-shell" tag to describe such dwi dataset.

By always using datatype tags to add specificity, Brainlife can correctly identify which datasets can be used for which Apps by examining dataset's datatype tags and App's input dataset tags. 

!!! hint
    Please consult the #datatype slack channel on Brainlife slack team for any datatype related questions.
