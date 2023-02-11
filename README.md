# eco-ci-co2-grid-intensity

This is a Github Action for checking the current grid intensity of the IP based location where the machine is running.

It takes the current external IP, queries the MaxMind Geo2LiteCity Database and then uses the CO2Signal API to get the current CO2 grid intensity at that latitude and longitude.


#### Required Inputs
`maxmind-account-id:`: The ID for your free Maxmind account
`maxmind-license-key`: The Maxmind API license key created by you in their dashboard
`co2signal-auth-token`: The free CO2Signal API Auth Token

#### Outputs:
`grid-intensity`: The grid intensity in gCO2e/kWh

#### Example Use

```
# This is a basic workflow to help you get started with Actions

name: CO2 grid intensity Test

# Controls when the workflow will run
on:
  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # This workflow contains a single job called "build"
  build:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest

    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
    
      - id: eco-ci-co2-grid-intensity
        uses: green-coding-berlin/eco-ci-co2-grid-intensity@main
        with:
          maxmind-account-id: ${{ secrets.MAXMIND_ACCOUNT_ID }}
          maxmind-license-key: ${{ secrets.MAXMIND_LICENSE_KEY }}
          co2signal-auth-token: ${{ secrets.CO2SIGNAL_AUTH_TOKEN }}
      - shell: bash
        run: |
          echo "Your grid intensity is: ${{ steps.eco-ci-co2-grid-intensity.outputs.grid-intensity }}" >> $GITHUB_STEP_SUMMARY
```
