## Resources

- [Google Interview University](https://github.com/jwasham/google-interview-university#system-design-scalability-data-handling)
- [High Scalability examples](https://www.hiredintech.com/classrooms/system-design/lesson/61)
- [HiredInTech](https://www.hiredintech.com/classrooms/system-design/lesson/60)
- Go through [this video](https://www.youtube.com/watch?v=PJKYqLP6MRE) 

### Communication

What do they look for?

**Problem solving skills**

- How many clarify problem statement
- Ask questions and not make assumptions
- Mention edge cases
- Walk through the problem one thing at a time
- Code beautifully (not syntax wise though)
- Test the code once code completed and then only say it is done

**Working on large systems** 

- How will you design systems
- High QPS what will you do
- If any issue how do you go about resolving it

### System Design

**Sample Design questions**

- Tic Tac Toe
- Minesweeper
- Web Crawler
- TinyURL
- Air Traffic Controller
- Conference Scheduler
- Adhaar enrollment
- Healthcare data collection by government (Thoughtworks)

### Approach

- Clarify assumptions regarding domain - features required
- Expected traffic/volume/data (calculate/assume)
- Expected frequency or repeated calls - Pre-processing of data (eg: Dictionary)
- Constraints - Bandwidth/Latency, CPU/Memory/Disk
- Scaling - Vertical / Horizontal(duplicate/load-balancing, key-hash, directory-based, service-based)
- Caching - LRU, LFU, Timeouts
- Heavy writes - Asynchronous (Task Queues)			
- Single point of failures
- Monitoring/Analytics
- Staggered/Back-pressure
- Batching/Chunking
- Geographic split (behavioral/regulatory)
- CDN (static content)

### Scalability
 
- Horizontal scaling
- Caching
- Load balancing
- Database replication
- Database partitioning
- NoSQL
- Asynchronous (Job Queues)

