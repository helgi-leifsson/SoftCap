# SoftCap
A Timed Rebeca model of a Hadoop SoftCap (Fair Scheduler) mechanism

The model works by jobs entering the queue at the Resource Manager. Every unit of time the RM finds the job using the least resources and if the job is not using any, finds a free container and starts an AppMaster for the job. When an AM starts, it requests resources for its map tasks and waits for them to be allocated by the RM.
If the job using the least resources is already running an AM and has requested resources, the RM allocates a container for it and continues looking for the job using the least resources.

Once either all containers have been allocated or there are no resource requests remaining, the RM sends a single message to every AM that had allocations made to it, listing the containers it should use to run its tasks. The AM then messages these containers to run the tasks.

When an AM completes its map phase it requests resources for its reduce tasks, and when the reduce phase completes the AM sends a job complete message to the RM.
