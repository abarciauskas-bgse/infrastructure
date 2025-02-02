
# List of running hubs

% NOTE: The CSV files used by this page are generated by `docs/scripts/render_hubs.py`

Here's a list of running hubs and some statistics about them.
It is automatically generated from the config stored in the [`config/clusters` folder of the `infrastructure` repository](https://github.com/2i2c-org/infrastructure/tree/HEAD/config/clusters) and can therefore be limited in the information it provides.

```{admonition} Missing information for Azure hubs
Hubs that have `kubeconfig` listed as their provider are most likely running on Azure.
The reason `kubeconfig` is listed as a provider is because that is the mechanism we are using to authenticate to that cluster in the case where we do not have a Service Principal.

Unlike GCP and AWS, Azure does not require the location for authentication and it is therefore not listed in our config files and hence cannot be populated in this table.
```

## Table of all running hubs

A table of all running hubs across all of our clusters.

<div class="full-width hubs-table">

```{csv-table}
:header-rows: 1
:file: ../tmp/hub-table.csv
```

</div>


## Hub options table

<div class="full-width hub-options-table">

```{csv-table}
:header-rows: 1
:file: ../tmp/hub-options-table.csv
```

</div>

## Community hub statistics

Summary statistics of the communities we are serving with with hubs, broken down by cluster and cloud provider.

```{csv-table}
:header-rows: 1
:file: ../tmp/hub-stats.csv
```

% DataTables config to make the table above look nice
<link rel="stylesheet"
      href="https://cdn.datatables.net/1.10.24/css/jquery.dataTables.min.css">
<script type="text/javascript"
        src="https://cdn.datatables.net/1.10.24/js/jquery.dataTables.min.js"></script>

<script>
var checkbox = function (data) {
    var c = data.toString().trim()
    console.log(c)
    if (c == "<p>True</p>") {
        return '<input type="checkbox" class="editor-active" onclick="return false;" checked>';
    }
    else {
        return '<input type="checkbox" onclick="return false;" class="editor-active">';
    }
}

$(document).ready( function () {
    $('.hub-options-table table').DataTable( {
        "order": [[ 0, "template" ]],
        "pageLength": 25,
        "columns": [
            null, // domain column, nothing special configured
            {"render": checkbox}, // dedicated cluster column
            {"render": checkbox}, // dedicated nodepool column
            {"render": checkbox}, // user buckets (scratch/persistent) column
            {"render": checkbox}, // requestor pays for buckets storage column
            null, // authenticator column
            {"render": checkbox}, // user anonymisation column
            {"render": checkbox}, // allusers access column
            {"render": checkbox}, // community domain column
            {"render": checkbox}, // custom login page column
            {"render": checkbox}, // custom html pages column
            {"render": checkbox}, // gh-scoped-creds column
        ]
    });

    $('.hubs-table table').DataTable( {
        "order": [[ 0, "template" ]],
        "pageLength": 25,
    });
} );
</script>

% Make the tables a little bit more compact since there's a lot of text
<style>
    table {
        font-size: .7em;
    }

    table th, table td {
        padding: 0;
    }
</style>
