1. How does the remote client determine when a command's output is fully received from the server, and what techniques can be used to handle partial reads or ensure complete message transmission?

The client checks for the EOF character to know that it has fully received the output from the server. If only part of the output is read, the client will know this because it will not receive the EOF character yet. The client can keep calling recv until it gets the EOF character.

2. This week's lecture on TCP explains that it is a reliable stream protocol rather than a message-oriented one. Since TCP does not preserve message boundaries, how should a networked shell protocol define and detect the beginning and end of a command sent over a TCP connection? What challenges arise if this is not handled correctly?

The protocol should define a special character to delineate the end of a command. That way the shell will know to handle only the data up to the special character and no more. If there is any more data after that character, it should hold it in a buffer until the first command is finished. Then it can call recv again and add to that buffer whatever data it receives.

3. Describe the general differences between stateful and stateless protocols.

A stateful protocol keeps track of information between requests so that the context of previous requests can be used in some way with a new request. A stateless protocol does not keep any information from previous requests, so each new request has to be handled without knowing any context about previous requests.

4. Our lecture this week stated that UDP is "unreliable". If that is the case, why would we ever use it?

Since UDP is faster, it is better in cases where we need to transmit and receive the data as fast as possible, such as with streaming audio or video. In those cases, we can implement error correction to deal with lost data, or just skip whatever data is missing if there is a large piece missing. 

5. What interface/abstraction is provided by the operating system to enable applications to use network communications?

The OS uses sockets to allow applications to use network communication. This way, much of the application can use the socket file descriptors the same way that it uses other file descriptors.