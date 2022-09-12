---
layout: page
title: "bbb"
permalink: /bbb/
---
# BBB
BBB , or Blorgon Bloberblating Blybtem, named after a certain middleware masquerading as an operating system , (that has inconveniced the author for a long time ) is a little, extremely simple IPC system that focuses only on simplicity. ONLY ON SIMPLICITY!. If you want something fast, or optimized, or reliable, use something else. This software was created more or less by an idiot who has no idea what he is doing. And it took him waaaay longer than it would normally take someone to make. It works using sockets for IPC.The arbiter listens at port 8008. It is also content agnostic, BBB doesnt care what data is sent , or in what format the user sends it. It is up to the user to parse and decode the data. BBB just gives you the start and end indices of the data.

BBB consists mainly of a parser , for which different implementations have to be written for different langauges. The author has developed implementations for python and rust.
The author would love for someone to make an implementation in c or lua. So if you wanna contribute to this monstrosity, please!

Another thing the author would like to state (emphasise , infact) is that this project , only aims to create a simple IPC system, one that can be easily understood. It should not become more complicated than it currently is. It must remain really simple.

The author understands that the description provided here is quite vague. They shall be updated once the project has been tested in the real world on a real world system.

## PROTOCOL 
The BBB protocol maybe obtained [here](https://jfarhanm.github.io/protocol/)

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

