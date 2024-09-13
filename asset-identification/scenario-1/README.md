# Scenario 1: Initial Discovery

This scenario focused on how a solution performed during the initial discovery of an environment that the solution had not previously identified. Three different profiles tested the solution across a variety of settings:

* **Scenario 1.A**: Conservative—tuned to be the least likely to affect ongoing operations of the underlying ICS or negatively affect fragile OT devices
* **Scenario 1.B**: Default—the default or recommended settings of the product
* **Scenario 1.C**: In Depth—tuned to identify as much information as possible, specifically about OT assets in
the PV plant and substation.

In each decimal sub-scenario, the pre-conditions, procedures, data collected, and evaluation criteria are the same. The only difference is which settings that the solution is configured to use.

## Pre-conditions

* Before each run, the solution should be fully installed and configured. However, the solution should have no previous exposure to the BOE. Some examples of pre-conditions:
  * solution agents are installed in their respective subnets
  * solution server is installed and configured
  * solution is configured with credentials or permisions that it requires
  * firewall rules are updated such that the solution can function as designed

## Procedures

### Step 1 - Check AOE

Make sure that all assets in the environment are available and functioning as expected.

CECA Cohort 2 accomplishes this with the [phenix state of health app](https://phenix.sceptre.dev/latest/state-of-health/#sample-soh-scenario-config). Custom tests for each host ensure that connections and services are available and functioning as expected.

### Step 2 - Setup Solution

Run any commands to set up or configure the solution. This includes updates to the specific settings for either Scenario 1A, 1B, or 1C. In addition, baseline information about the solution is collected to validate and record its settings and status before the test is started.

CECA Cohort 2 accomplishes this with API calls, CLI commands, or GUI interactions particularized to the solution being tested. 

### Step 3 - Start Disruption to Operations Record

Record the availability of each asset throughout the scan to ensure active scanning does not affect any assets.

CECA Cohort 2 accomplishes this with [`fping`](https://fping.org/).

```bash
fping -l -p 1000 -t 300 -r 3 -D -e -f /root/monitor-ips.txt > /root/disruption-results.txt 2>&1
```

### Step 4 - Start `tcpdump` on solution agent(s) and firewalls

Start collecting network traffic on a solution's agents and firewalls.

CECA Cohort 2 accomplishes this with the [scorch](https://phenix.sceptre.dev/latest/scorch/) `tcpdump` component.

### Step 5 - Start Timer

Record the time when the solution begins running.

CECA Cohort 2 accomplishes this with `date +%s.%N > /root/timing.txt`

### Step 6 - Start the Solution Scan

Start the solution's discovery.

CECA Cohort 2 accomplishes this with API calls, CLI commands, or GUI interactions particularized to the solution being tested. 

### Step 7 - Wait until the Solution is Complete

Wait until the discovery reports to be completed and then proceed.

CECA Cohort 2 accomplishes this with API calls, CLI commands, or GUI interactions particularized to the solution being tested. 

### Step 8 - Stop Timer

Record the time when the solution is done running, ending the timer started in step 4.

CECA Cohort 2 accomplishes this with `date +%s.%N >> /root/timing.txt`

### Step 9 - Stop `tcpdump` on solution agent(s) and firewalls

End the `tcpdumps` started in step 4.

### Setp 10 - Stop Disruption to Operations Record

Stop recording availability of assets that was started in step 3.

### Step 11 - Extract and Save Results

Record the solution state at the end of the test.

CECA Cohort 2 accomplishes this with API calls, CLI commands, or GUI interactions particularized to the solution being tested, and the [scorch](https://phenix.sceptre.dev/latest/scorch/) `cc` component to extract files.

## Data Collected

Once the above procedures are completed, the following sources of data are retrieved and archived for further analysis:

* Solution Database (`inventory.csv`)
* Results of Timer (`timing.txt`)
* Results of Disruption to Operations (`*-disruption-results.txt`)
* Solution Traffic (`*.pcap`)
* AOE status (`soh.json`)
* Solution specific settings, status messages, etc.

## Evaluation Criteria

* Timing
* Inventory accuracy
* Data richness
* Additional network load
* Disruption of operations