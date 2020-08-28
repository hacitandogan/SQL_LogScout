
# Introduction
SQL LogScout allows you to collect diagnostic logs from your SQL Server system to help you and Microsoft technical support engineers (CSS) to resolve SQL Server technical incidents faster. It is a light, script-based, open-source tool that is version-agnostic. SQL LogScout discovers the SQL Server instances running locally on the system (including FCI and AG instances) and offers you a list to choose from. 

# Usage

1. Start the tool via SQL_LogScout.cmd when the issue is happening
1. Select which SQL instance you want to diagnose from a numbered list
1. Pick the Scenario from a menu list (based on the issue under investigation)
1. Stop the collection when you are ready (by typing "stop")

## Parameters
SQL_LogScout.cmd accepts two optional parameters:
1. **DebugLevel** - values are between 0 and 5 (default 0). Debug level provides detail on what is executed on the system and is mostly for troubleshooting and debugging SQL LogScout
1. **Scenario** - possible values are "Basic", "GeneralPerf", "DetailedPerf", "AlwaysOn","Replication" (no default). For more information on each scenario see [Scenarios](#scenarios)

## Scenarios
1. **Basic scenario** collects snapshot logs. It captures information:
   - Running drivers on the system
   - System information (systeminfo.exe)
   - Miscelaneous sql configuration (sp_configure, databases, etc)
   - Processes running on the system (Tasklist.exe)
   - Current active PowerPlan
   - Installed Windows Hotfixes
   - Running filter drivers
   - Event logs (system and application)
1. **GeneralPerf scenario** collects all the Basic scenario logs as well as some long-term, continuos logs (until SQL LogScout is stopped).
   - Basic scenario
   - Performance Monitor counters for SQL Server instance and general OS counters
   - Extended Event trace captures batch-level starting/completed events, errors and warnings, log growth/shrink, lock escalation and timeout, deadlock, login/logout
   - List of actively-running SQL traces and Xevents
   - Snapshots of SQL DMVs that track waits/blocking and high CPU queries
   - Query Data Store info (if that is active)
   - Tempdb contention info from SQL DMVs/system views
   - Linked Server metadata (SQL DMVs/system views)
   - Service Broker configuration information (SQL DMVs/system views)
1. **DetailedPerf scenario** collects the same info that the GeneralPerf scenario. The difference is in the Extended event trace
   - GeneralPerf scenario
   - Extended Event trace captures same as GeneralPerf. In addition in the same trace it captures statement level starting/completed events and actual XML query plans (for completed queries)
1. **AlwaysOn scenario** collects all the Basic scenario logs as well as Always On configuration information from DMVs
   - Basic scenario
   - Always On diagnostic info (SQL DMVs/system views)
1. **Replication scenario** collects all the Basic scenario logs plus SQL Replication, Change Data Capture (CDC) and Change Tracking (CT) information
   - Basic Scenario
   - Replication, CDC, CT diagnostic info (SQL DMVs/system views)


# Sample output

```bash
     ======================================================================================================
              #####   #####  #          #                      #####
             #     # #     # #          #        ####   ####  #     #  ####   ####  #    # #####
             #       #     # #          #       #    # #    # #       #    # #    # #    #   #
              #####  #     # #          #       #    # #       #####  #      #    # #    #   #
                   # #   # # #          #       #    # #  ###       # #      #    # #    #   #
             #     # #    #  #          #       #    # #    # #     # #    # #    # #    #   #
              #####   #### # #######    #######  ####   ####   #####   ####   ####   ####    #
     ======================================================================================================

2020-08-27 11:58:57.738	INFO	Initializing log C:\temp\pssdiag\Test 2\output\internal\##SQLDIAG.LOG 
2020-08-27 11:58:54.930	INFO	SQL LogScout version: 1.1.0 
2020-08-27 11:58:55.031	INFO	The Present folder for this collection is C:\temp\pssdiag\Test 2 
2020-08-27 11:58:55.046	INFO	Output path: C:\temp\pssdiag\Test 2\output\ 
2020-08-27 11:58:55.046	INFO	The Error files path is C:\temp\pssdiag\Test 2\output\internal\ 
2020-08-27 11:58:55.046	INFO	 
2020-08-27 11:58:55.062	WARN	It appears that output folder C:\temp\pssdiag\Test 2\output\ has been used before. 
2020-08-27 11:58:55.062	WARN	DELETE the files it contains (Y/N)? 
2020-08-27 11:58:57.607	INFO	Console input: y 
2020-08-27 11:58:58.108	INFO	Discovered the following SQL Server instance(s)
 
2020-08-27 11:58:58.108	INFO	 
2020-08-27 11:58:58.108	INFO	ID	SQL Instance Name 
2020-08-27 11:58:58.108	INFO	--	---------------- 
2020-08-27 11:58:58.108	INFO	0 	 DbServerMachine\SQL2014 
2020-08-27 11:58:58.124	INFO	1 	 DbServerMachine 
2020-08-27 11:58:58.124	INFO	2 	 DbServerMachine\SQL2017 
2020-08-27 11:58:58.124	INFO	 
2020-08-27 11:58:58.124	WARN	Enter the ID of the SQL instance for which you want to collect diagnostic data. Then press Enter 
2020-08-27 11:59:01.549	INFO	Console input: 0 
2020-08-27 11:59:01.565	INFO	You selected instance 'DbServerMachine\SQL2014' to collect diagnostic data.  
2020-08-27 11:59:01.649	INFO	Confirmed that MYDOMAIN\Joseph has VIEW SERVER STATE on SQL Server Instance DbServerMachine\SQL2014 
2020-08-27 11:59:01.665	INFO	LogmanConfig.txt copied to  C:\temp\pssdiag\Test 2\output\internal\LogmanConfig.txt 
2020-08-27 11:59:01.734	INFO	 
2020-08-27 11:59:01.734	INFO	Initiating diagnostics collection...  
2020-08-27 11:59:01.734	INFO	Please select one of the following scenarios:
 
2020-08-27 11:59:01.734	INFO	 
2020-08-27 11:59:01.749	INFO	ID   Scenario 
2020-08-27 11:59:01.749	INFO	--   --------------- 
2020-08-27 11:59:01.749	INFO	0    Basic (no performance data) 
2020-08-27 11:59:01.749	INFO	1    General Performance (recommended for most cases) 
2020-08-27 11:59:01.749	INFO	2    Detailed Performance (statement level and query plans) 
2020-08-27 11:59:01.749	INFO	3    Replication 
2020-08-27 11:59:01.749	INFO	4    AlwaysON 
2020-08-27 11:59:01.749	INFO	 
2020-08-27 11:59:01.765	WARN	Enter the Scenario ID for which you want to collect diagnostic data. Then press Enter 
2020-08-27 11:59:11.613	INFO	Console input: 1 
2020-08-27 11:59:11.629	INFO	Executing Collector: RunningDrivers 
2020-08-27 11:59:12.742	INFO	Executing Collector: SystemInfo_Summary 
2020-08-27 11:59:13.797	INFO	Executing Collector: MiscPssdiagInfo 
2020-08-27 11:59:15.819	INFO	Executing Collector: TaskListVerbose 
2020-08-27 11:59:15.850	INFO	Executing Collector: TaskListServices 
2020-08-27 11:59:15.872	INFO	Executing Collector: collecterrorlog 
2020-08-27 11:59:17.908	INFO	Executing Collector: PowerPlan 
2020-08-27 11:59:18.008	INFO	Executing Collector: WindowsHotfixes 
2020-08-27 11:59:18.309	INFO	Executing Collector: FLTMC_Filters 
2020-08-27 11:59:18.325	INFO	Executing Collector: FLTMC_Instances 
2020-08-27 11:59:20.347	INFO	Executing Collector: GetEventLogs 
2020-08-27 11:59:27.783	INFO	Executing Collector: Perfmon 
2020-08-27 11:59:28.824	INFO	Executing Collector: pssdiag_xevent 
2020-08-27 11:59:30.877	INFO	Executing Collector: pssdiag_xevent_general_target 
2020-08-27 11:59:30.893	INFO	Executing Collector: pssdiag_xevent_Start 
2020-08-27 11:59:30.908	INFO	Executing Collector: ExistingProfilerXeventTraces 
2020-08-27 11:59:32.937	INFO	Executing Collector: HighCPU_perfstats 
2020-08-27 11:59:32.953	INFO	Executing Collector: SQLServerPerfStats 
2020-08-27 11:59:34.990	INFO	Executing Collector: SQLServerPerfStatsSnapshotStartup 
2020-08-27 11:59:35.022	INFO	Executing Collector: Query Store 
2020-08-27 11:59:37.032	INFO	Executing Collector: TempDBAnalysis 
2020-08-27 11:59:37.047	INFO	Executing Collector: linked_server_config 
2020-08-27 11:59:37.085	INFO	Executing Collector: SSB_pssdiag 
2020-08-27 11:59:37.116	INFO	Diagnostic collection started. 
2020-08-27 11:59:37.116	INFO	 
2020-08-27 11:59:37.116	WARN	Please type 'STOP' or 'stop' to terminate the diagnostics collection when you finished capturing the issue 
2020-08-27 11:59:53.639	INFO	Console input: stop 
2020-08-27 11:59:53.654	INFO	Shutting down the collector 
2020-08-27 11:59:53.654	INFO	Stopping Collector: SQLServerPerfStatsSnapshotShutdown 
2020-08-27 11:59:53.670	INFO	Stopping Collector: xevents_stop 
2020-08-27 11:59:53.686	INFO	Stopping Collector: PerfmonStop 
2020-08-27 11:59:56.714	INFO	Running: killpssdiagSessions 
2020-08-27 11:59:56.720	INFO	Waiting 5 seconds to ensure files are written to and closed by any program including anti-virus... 
2020-08-27 12:00:01.731	INFO	Ending data collection 
```

# Output folders

**Output folder**: All the log files are collected in the \output folder. These include perfmon log (.BLG), event logs, system information, extended event (.XEL), etc. 

**Internal folder**: The \internal folder stores error log files as well as the main activity log file for SQL LogScout (##SQLDIAG.LOG). If those files are not empty, they contain information about whether a particular data-collector failed or produced some result (not necessarily failure). If the main script produces some errors in the console, those are redirected to a file ##STDERR.LOG and the contents of that file is displayed in the console after the main script completes execution.

# Targeted SQL instances

Data is collected from the SQL instance you selected locally on the machine where SQL LogScout runs. SQL LogScout does not capture data on remote machines. You are prompted to pick a SQL Server instance you want to target. The SQL Server-specific data collection comes from a single instance only. 