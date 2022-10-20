# Operation: AIDO Evaluations {#autolab-2-aido-eval status=draft}

<div class='requirements' markdown="1">

Requires: [](#autolab-2-localization) is setup.

Requires: In addition to the desktop/laptop requirement for localization, an NVIDIA GPU is needed, drivers should be installed

Results: Can run AIDO submissions and report results.

<!-- Next Steps: put next steps here -->
</div>


## AIDO evaluator

The AIDO evaluator, which is the process that talks to the AIDO challenges server and gets assigned evaluation jobs. After running an evaluation experiment, it uploads the artifacts (rosbags, logs, videos, localization results) for the AIDO challenge server to further process.

### Run localization in REST mode

This creates REST APIs that the AIDO evaluator process will use to run localization experiments with the Autolab. From the root of the `duckietown/dt-autolab-localization` repository:

    $ dts devel build
    $ dts devel run -f -X -L REST -- --hostname ETHlargeloop

### Run the AIDO evaluator

Clone the Github repository `duckietown/dt-aido-autolab-evaluator`.

    $ git clone https://github.com/duckietown/dt-aido-autolab-evaluator.git

The evaluator needs a directory, `/data`, to store temporary files in. Make sure to create it before running the evaluator.

    $ mkdir -p /data

Then, from the root of the repository, run:

    $ dts devel build -f

TODO: the command to run needs cleanup and verification

```bash
dts devel run \
    -A aido=5 \
    -A autolab=![name_of_the_map] \
    -A token=![your_duckietown_token] \
    -A stage \
    -X \
    -- -v /var/run/docker.sock:/var/run/docker.sock \
    -e DEBUG=1
```

## Troubleshooting
TODO: write known issues and resolutions