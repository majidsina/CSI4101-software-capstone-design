## A network-aware load balancer using DRL

### Things To Do:  
1. Decide where drl server lives. Also it should be called load balancer which has a DRL solution.
2. Make emulator switchable. That is the entire project could work without emulator if all clients/servers are properly set.
3. Include dockerfile of the service server to automate deployment. Also probably include some bash command for multiple docker each serving a single model.
4. Objectize(Class) request metadata. There are some specific 'methods' involved with those data.
5. Overhaul the content and structure of 'server_states'
6. Implement DRL and tune it.


**client_req.py:**  
1. Load ImageNet validation images
2. Generate paremeterized(request interval, expected accuracy/time, etc) request distribution

**emulator.py:**  
1. Handle client request  
    1. Collect request meta-info and server states info
    2. Send them to DRL server to decide which (server:service) to use.
    3. Listen for DRL server's response(action).
    4. Make the actual service request while emulating network overhead.
2. Monitor server states
    1. Collect server states from each server and make them send-ready.
3. Emulate networking between servers.
    1. Interface to control/paremeterize network overhead
    2. Emulate delayed/limited transfer
    3. Emulate server states(only networking stats)

**evaluater.py:**  
1. Load ImageNet validation solutions.
2. Identify request and rate correspoding service response by accuracy&time.

**server_monitor.py:**  
1. Collect server's state.
2. Send it to emulator.

**DRL.py:**  
Not considred yet.
