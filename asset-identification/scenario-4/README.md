# Scenario 4: Scale Discovery

This scenario focused on how a solution performs at scale. The previous three scenarios were all run in the same PV and substation environment with several tens of devices. To stress the solution and test how it performs at scale, CECA created the AMI environment with 3,948 different AMI devices in a single "flat" subnet (/20 in classless inter-domain routing (CIDR) notation). Scenario 4 consisted of two consecutive scans. First, the solution was activated to identify all of the existing assets in the environment without any previous knowledge. Second, a single additional device was added to the network, and the solution was again activated to identify all assets in the environment, including the new device. In both scans, the solution used the default settings, as in Scenario 1B. Scenario 4 magnifies both the time that the solution takes to identify a single device and the amount of additional network traffic that the solution adds to the infrastructure when identifying a single asset. In addition, Scenario 4 provides an opportunity to test a solution’s ability to identify a new device in a much larger environment. Note that Scenario 4 was not evaluating the accuracy or richness of the data identified.

## Pre-conditions

The pre-conditions for the first and second run of this scenario mirror the pre-conditions for [scenario 1](/asset-identification/scenario-1/README.md#pre-conditions) and [scenario 2](/asset-identification/scenario-2/README.md#pre-conditions) respectively.

Before the first run:

* The solution should be fully installed and configured. However, the solution should have no previous exposure to the BOE. Some examples of pre-conditions:
    * solution agents are installed in their respective subnets
    * solution server is installed and configured
    * solution is configured with credentials or permisions that it requires
    * firewall rules are updated such that the solution can function as designed

Before the second run:

* The first run must be complete and the  solution must be onboarded. If any information was incorrectly identified or not identified in scenario 1, those deficiencies should be manually corrected.
* The solution should be configured to generate alerts (to the extent that the solution allows) when it identifies new devices.
* An additional 'attacker' VM should be added to the environment.

## Procedures

Scenario 4 is similar to previous scenarios, except that it consists of two runs conducted in sequence (run A and run B).

### *Run A*

### Step 1 - Setup Solution Run A

Run any commands to set up or configure the solution. In addition, baseline information about the solution is collected to validate and record its settings and status before the test is started.

CECA Cohort 2 accomplishes this with API calls, CLI commands, or GUI interactions particularized to the solution being tested.

### Step 2 - Start `tcpdump` on solution agent(s) and firewalls A

Start collecting network traffic on a solution's agents and firewalls.

CECA Cohort 2 accomplishes this with the [scorch](https://phenix.sceptre.dev/latest/scorch/) `tcpdump` component.

### Step 5 - Start Timer A

Record the time when the solution begins running.

CECA Cohort 2 accomplishes this with `date +%s.%N > /root/timing.txt`

### Step 6 - Start the Solution Scan A

Start the solution's discovery.

CECA Cohort 2 accomplishes this with API calls, CLI commands, or GUI interactions particularized to the solution being tested.

### Step 7 - Wait until the Solution is Complete with Run A

Wait until the discovery reports to be completed and then proceed.

CECA Cohort 2 accomplishes this with API calls, CLI commands, or GUI interactions particularized to the solution being tested.

### Step 8 - Stop Timer A

Record the time when the solution is done running, ending the timer started in step 5.

CECA Cohort 2 accomplishes this with `date +%s.%N >> /root/timing.txt`

### Step 9 - Stop `tcpdump` on solution agent(s) and firewalls A

End the `tcpdumps` started in step 4.

### Step 10 - Extract and Save Results A

Record the solution state at the end of test A.

CECA Cohort 2 accomplishes this with API calls, CLI commands, or GUI interactions particularized to the solution being tested, and the [scorch](https://phenix.sceptre.dev/latest/scorch/) `cc` component to extract files.

### *Run B*

### Step 11 - Connect Attacker

Add a single additional 'attacker' to the environment.

CECA Cohort 2 accomplishes this with the [scorch](https://phenix.sceptre.dev/latest/scorch/) `mm` to turn on the attacker VM.

### Step 12 - Baseline Solution Before Run B

Baseline information about the solution is collected to validate and record its settings and status before the run B is started.

CECA Cohort 2 accomplishes this with API calls, CLI commands, or GUI interactions particularized to the solution being tested.

### Step 13 - Create Alert

Create an alert for new devices found during this run.

CECA Cohort 2 accomplishes this with API calls, CLI commands, or GUI interactions particularized to the solution being tested.

### Step 14 - Start `tcpdump` on solution agent(s) and firewalls B

Start collecting network traffic on a solution's agents and firewalls.

CECA Cohort 2 accomplishes this with the [scorch](https://phenix.sceptre.dev/latest/scorch/) `tcpdump` component.

### Step 15 - Start Timer B

Record the time when the solution begins running.

CECA Cohort 2 accomplishes this with `date > /root/timing.txt`

### Step 16 - Start the Solution Scan B

Start the solution's discovery.

CECA Cohort 2 accomplishes this with API calls, CLI commands, or GUI interactions particularized to the solution being tested.

### Step 17 - Wait until the Solution is Complete with Run B

Wait until the discovery reports to be completed and then proceed.

CECA Cohort 2 accomplishes this with API calls, CLI commands, or GUI interactions particularized to the solution being tested.

### Step 18 - Stop Timer B

Record the time when the solution is done running, ending the timer started in step 15.

CECA Cohort 2 accomplishes this with `date >> /root/timing.txt`

### Step 19 - Stop `tcpdump` on solution agent(s) and firewalls

End the `tcpdumps` started in step 14.

### Step 20 - Extract and Save Results B

Record the solution state at the end of test A.

CECA Cohort 2 accomplishes this with API calls, CLI commands, or GUI interactions particularized to the solution being tested, and the [scorch](https://phenix.sceptre.dev/latest/scorch/) `cc` component to extract files.

### Step 21 - Check Alert

Check for alerts for the new devices found during this test.

CECA Cohort 2 accomplishes this with API calls, CLI commands, or GUI interactions particularized to the solution being tested.

## Data Collected

Once the above procedures are completed, the following sources of data are retrieved and archived for further analysis:

* Solution Database (`inventory.csv`)
* Results of Timer (`timing.txt`)
* Solution alert (`alert.png`)
* Solution Traffic (`*.pcap`)
* Solution specific settings, status messages, etc.

## Evaluation Criteria

* Timing
* Inventory accuracy
* Additional network load
* Alert
* Change Detection
