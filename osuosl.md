---
layout: page 
title: IPMI Management Console
permalink: /osuosl/
---

The following page serves as a wiki for my GSoC '14 project with the OSU OSL.

### Some useful links

   * Code and version history for this page can be found [here](https://github.com/emaadmanzoor/blog/blob/gh-pages/osuosl.md).
   * You can find my proposal [here](http://www.google-melange.com/gsoc/proposal/review/student/google/gsoc2014/emaadmanzoor/5724160613416960).
   * Repository for the code under the OSU OSL [Github organization](https://github.com/osuosl). `TODO`
      * Until we move them under the OSUOSL organization, the repositories will be here: [igor-rest-api](https://github.com/emaadmanzoor/igor-rest-api), [igor-cli](https://github.com/emaadmanzoor/igor-cli)
   * OSL IPMI test machine. `TODO`

### Current Tasks

   * `TODO` Get access to an IPMI-enabled machine
      * *Hypervisors supporting IPMI?* Until I get access to a physical machine,
        I supposed having a VM on a hypervisor that implements
        a virtual IPMI interface would be useful, but neither KVM/QEMU or Virtualbox support this.
   * Discuss initial REST API and CLI design, REST service hosting
      * An initial implementation is available [here](https://github.com/emaadmanzoor/igor-rest-api).
   * Implement the `login` and `power` REST endpoints and CLI commands `TODO`
      * An implementation will be available soon [here](https://github.com/emaadmanzoor/igor-rest-cli).

## Design

The standard CLI for IPMI-enabled machines is [ipmitool](http://sourceforge.net/projects/ipmitool/). Since we
expect access from devices that may not have `ipmitool` available (eg. mobile phones), it makes sense to provide
a universal REST API that is served from an OSL machine.

### REST API

In the REST paradigm, interactions are with *resources* via HTTP *verbs*. In our case, resources could be
machines, machine devices/logs exposed by IPMI and users. The verbs are HTTP *GET*, *PUT*, *POST* etc.
that define different interactions with these resources.

   * `/login/`: Accepts a username/password combination, issues an auth token on success. All future
     IPMI requests reuse this auth token.
   * `/power/`: Powers on, off or cycle the machine. This wraps the `ipmitool power status|on|off|cycle|reset`
     commands.
   * `/console/`: Returns a persistent connection streaming the output of the SOL console. This wraps
     the `ipmitool sol activate|deactivate` commands.
   * `/sensors/`: Provides sensor readings. This wraps the `ipmitool sdr` commands.
   * `/log/`: Returns the sensor event log. This wraps the `ipmitool sel` commands.

### CLI

I plan for the CLI to make calls to the REST API, retreive the JSON response and format the output
in a suitable way for the screen. The CLI commands will look like the following:

{% highlight bash %}
igor login
igor power -h osl0[1-6] status|on|off|cycle|reset
igor console
igor sensors
igor log
{% endhighlight %}
