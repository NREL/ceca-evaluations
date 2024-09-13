# Scenario 3: Passive Discovery

This scenario focused on how a solution performs using exclusively passive methods to examine network traffic and
extract information from that traffic. Each of the previous scenarios tested a solution’s ability to identify assets using
active scanning, whereas this scenario isolated the solution’s passive capabilities.

## Pre-conditions

* Before each run, the solution should be fully installed and configured. However, the solution should have no previous exposure to the BOE. Some examples of pre-conditions:
* solution agents are installed in their respective subnets
* solution server is installed and configured
* solution is configured with credentials or permisions that it requires
* firewall rules are updated such that the solution can function as designed

## Procedures

Scenario 3 is similar to Scenario 1 except that the test waits for a pre-determined amount of time in step

### Step 1 - Check AOE

Make sure that all assets in the environment are available and functioning as expected.

CECA Cohort 2 accomplishes this with the [phenix state of health app](https://phenix.sceptre.dev/latest/state-of-health/#sample-soh-scenario-config). Custom tests for each host ensure that connections and services are available and functioning as expected.

### Step 2 - Setup Solution

Run any commands to set up or configure the solution. This includes updates to the specific settings for either Scenario 1A, 1B, or 1C. In addition, baseline information about the solution is collected to validate and record its settings and status before the test is started.

CECA Cohort 2 accomplishes this with API calls, CLI commands, or GUI interactions particularized to the solution being tested.

### Step 3 - Start `tcpdump` on solution agent(s) and firewalls

Start collecting network traffic on a solution's agents and firewalls.

CECA Cohort 2 accomplishes this with the [scorch](https://phenix.sceptre.dev/latest/scorch/) `tcpdump` component.

### Step 4 - Start the Solution Passive Sampling

Start the solution's discovery.

CECA Cohort 2 accomplishes this with API calls, CLI commands, or GUI interactions particularized to the solution being tested.

### Step 4 - Wait for 30 minutes

Wait for 30 minutes to give the solution ample time to observe and parse communications in the environment.

### Step 6 - Stop `tcpdump` on solution agent(s) and firewalls

End the `tcpdumps` started in step 3.

### Step 7 - Extract and Save Results

Record the solution state at the end of the test.

CECA Cohort 2 accomplishes this with API calls, CLI commands, or GUI interactions particularized to the solution being tested, and the [scorch](https://phenix.sceptre.dev/latest/scorch/) `cc` component to extract files.

## Data Collected

Once the above procedures are completed, the following sources of data are retrieved and archived for further analysis:

* Solution Database (`inventory.csv`)
* Solution Traffic (`*.pcap`)
* AOE status (`soh.json`)
* Solution specific settings, status messages, etc.

## Evaluation Criteria

* Inventory accuracy
* Data richness
* Additional network load
