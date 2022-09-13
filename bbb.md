---
layout: page
title: "bbb"
permalink: /bbb/
---
# BBB
BBB, or Blorgon Bloberblating Blybtem, named after a certain middleware masquerading as an operating system, (that has inconveniced the author for a long time ) is a little, extremely simple IPC system that focuses only on simplicity. ONLY ON SIMPLICITY!. If you want something fast, or optimized, or reliable, use something else. This software was created more or less by an idiot who has no idea what he is doing. And it took him waaaay longer than it would normally take someone to make. 

BBB works using sockets for IPC. An arbiter, which is part of BBB listens at port 8008.BBB is also content agnostic, BBB doesnt care what data is sent, or in what format the user sends it. It is up to the user to parse and decode the data. BBB just gives you the start and end indices of the data.

BBB consists mainly of a parser , for which different implementations have to be written for different languages. The author has developed implementations for python and rust.
The author would love for someone to make an implementation in c or lua. So if you wanna contribute to this monstrosity, please!

Another thing the author would like to state (emphasise , infact) is that this project only aims to create a simple IPC system, one that can be easily understood. It should not become more complicated than it currently is. It must remain really simple.

The author understands that the description provided here is quite vague. It shall be updated once the project has been tested in the real world on a real world system.

## PROTOCOL 
The BBB protocol maybe obtained [here](https://jfarhanm.github.io/protocol/)
The output after BBB has parsed a packet is as follows
```
{
  header:u8
  data_size:u64
  result_type:(u8,u8)
  data:(u64,u64) // start and end of relevant data in the packet
  text_list:[string]  
}
```

## Project Structure 
The following repositories hold the components of BBB
 - [parser](https://github.com/jfarhanm/bbb-parser)
 - [call generator](https://github.com/jfarhanm/bbb_call_gen)
 - [arbiter (bbb-core, you could call it)](https://github.com/jfarhanm/bbb)
 - [All the python client libraries](https://github.com/jfarhanm/bbb_python)

This project is still very much a WIP, and may take a while to become less shitty than it is now.

# IPC structure 
This project does have a focus on modularity , so there are different ways a user may go about implementing this directly , if all you need to do is communicate. The following diagrams illustrate this (apologies for being vague again):
```

                            BASIC COMMUNICATION STRUCTURE




                    ┌────────────────────────────────────────────┐
                    │                                            │
                    │                                            │
                    │                 ARBITER                    │
                    │                                            │
                    │                bbb-master                  │
                    │                                            │
                    │        (CONTAINS BBB CLIENT LIBRARY)       │
                    │                                            │
                    └────────────────────────────────────────────┘



                    ┌───────────────────────────────────────────┐
                    │                                           │
                    │            BBB CLIENT LIBRARY             │
                    │                                           │
                    │ ┌───────────────────────────────────────┐ │
                    │ │                                       │ │
                    │ │             connection                │ │
                    │ │                                       │ │
                    │ └───────────────────────────────────────┘ │
                    │                                           │
                    │ ┌───────────────────────────────────────┐ │
                    │ │                                       │ │
                    │ │               parser                  │ │
                    │ │                                       │ │
                    │ └───────────────────────────────────────┘ │
                    │                                           │
                    └───────────────────────────────────────────┘






                            SUPPORTED MODES
                        DIRECT MODE COMMUNICATION

                (may have to manually implement a listener)


                                                   ┌─────────────────────┐
   ┌─────────────────────┐                         │                     │
   │                     │                         │                     │
   │                     │                         │                     │
   │                     │                         │                     │
   │                     │    CALL                 │                     │
   │    BBB CLIENT A     │ ──────────────────────► │      BBB CLIENT B   │
   │                     │          CALLRESP       │                     │
   │                     │                         │                     │
   │                     │                         │                     │
   │                     │                         │                     │
   │                     │                         │                     │
   └─────────────────────┘                         └─────────────────────┘


                        ARBITER BASED COMMUNICATION


┌────────────┐
│            │                                               ┌────────────┐
│            │                                               │            │
│            │ CALL  SERVICE ID                              │            │
│  CLIENT C  ├─────────────────┐            ┌───────────────►│            │
│            │                 │            │ CALLRESP       │ SERVICE_C  │
│            │                 │            │ CALLER ID      │            │
│            │                 │            │                │            │
└────────────┘                 │            │                │            │
                               ▼            │                └────────────┘
┌────────────┐               ┌──────────────┴─┐
│            │               │                │              ┌────────────┐
│            │               │                │              │            │
│            │               │                │              │            │
│  CLIENT B  │               │    ARBITER     │              │            │
│            │─────────────► │                ├─────────────►│ SERVICE_B  │
│            │               │                │              │            │
│            │               │                │              │            │
└────────────┘               └───────────────┬┘              │            │
                               ▲             │               └────────────┘
┌────────────┐                 │             │
│            │                 │             │               ┌────────────┐
│            │                 │             │               │            │
│            │                 │             │               │            │
│  CLIENT A  │                 │             │               │            │
│            │                 │             └──────────────►│ SERVICE_A  │
│            ├─────────────────┘                             │            │
│            │                                               │            │
└────────────┘                                               │            │
                                                             └────────────┘

```


## Some Trivia 
"Blorgons" are the arch enemies of The Inspector on the long running British Science fiction show "Inspector Spacetime" from the show _community_ so here's a [link](https://community-sitcom.fandom.com/wiki/Blorgons). Watch _community_ btw , it's a great show ;).

The author also thinks that the name bodge_glue, which describes exactly what this project does, is a good fit here. The name may change in the future.
here's a little Tom scott video, explaining what a [bodge](https://www.youtube.com/watch?v=lIFE7h3m40U) is.

# FINAL WARNING
This project is in no way meant to be used in a production environment or to be shipped to a user. Ever. EVER!. Prototype with it , play with it , and have fun it with it. _It's not about money, it's about sending a message_

--jfm
