%title: How to deploy your HashiCorp stack with Ansible under 15 minutes
%author: Chris van Meer
%date: 2022-12-01

-> # HashiTalks 2022 Benelux <-





-> Welcome <-

-------------------------------------------------

-> # Agenda <-

* Introduction
    * `whoami`?
    * Why?
    * How?
* Setup
    * Goal
    * Infrastructure
    * General deployment
    * PKI
    * Consul
    * Vault
    * Nomad
    * Nomad / Vault integration && Nomad demo jobs
    * Demo
        * Traefik
        * Web app
* Resources
* Contact

-------------------------------------------------

-> # Introduction <-

chris@atcomputing ~ $ `whoami`

## Chris van Meer
Consultant at AT Computing

## Strong focus on
Networking, Ansible, HashiCorp portfolio

-------------------------------------------------

-> # Why? <-

* Most demos use dev mode
* TLS is always disabled
* Complete integration guide was missing
* Useable as quick test or demo environment
* Most demos use Terraform as default
* Needed something modular

-------------------------------------------------

-> # How? <-

```
                                                      
                             &@@@@@@@@@#              
                        @@@@@@@@@@@@@@@@@@@@&         
                     @@@@@@@@@@@@@@@@@@@@@@@@@@#      
                   @@@@@@@@@@@@@@.  @@@@@@@@@@@@@#    
                  @@@@@@@@@@@@@@.    @@@@@@@@@@@@@@   
                 @@@@@@@@@@@@@@.  @%  @@@@@@@@@@@@@@  
                #@@@@@@@@@@@@@   @@@#  @@@@@@@@@@@@@, 
                &@@@@@@@@@@@@     @@@#  @@@@@@@@@@@@* 
                *@@@@@@@@@@@   @@(   &#  @@@@@@@@@@@  
                 @@@@@@@@@@   @@@@@@%     @@@@@@@@@#  
                  @@@@@@@@   @@@@@@@@@@&   @@@@@@@%   
                   /@@@@@@@@@@@@@@@@@@@@@@@@@@@@@     
                     ,@@@@@@@@@@@@@@@@@@@@@@@@@       
                        ,@@@@@@@@@@@@@@@@@@@          
                              .#&@@&&(                
```

-------------------------------------------------

-> # Setup / Goal <-

* Create a high available stateless web app
* Load balanced
* Running TLS
* Integrate Consul, Vault and Nomad with each other
* Do it [on a local machine](For those who can't I've included a Terraform workflow for AWS as well)

-------------------------------------------------

-> # Setup / Infrastructure <-

```
       +---server1---+     +---server2---+     +---server3---+         
       |             |     |             |     |             |         
       | Consul (C)  |     | Consul (C)  |     | Consul (C)  |         
       | Vault  (V)  | <-> | Vault  (V)  | <-> | Vault  (V)  |         
       | Nomad  (N)  |     | Nomad  (N)  |     | Nomad  (N)  |         
       |             |     |             |     |             |         
       +-------------+     +-------------+     +-------------+         
              +-------------------+-------------------+
                                  |
                                  +                    
+---client1---+   +---client2---+   +---client3---+   +---client4---+
|             |   |             |   |             |   |             |
|  C + V + N  |   |  C + V + N  |   |  C + V + N  |   |  C + V + N  |
|  ---------  |   |  ---------  |   |  ---------  |   |  ---------  |
|   Traefik   |   |   Web App   |   |   Web App   |   |   Web App   |
|             |   |             |   |             |   |             |
+-------------+   +-------------+   +-------------+   +-------------+
```

-------------------------------------------------

-> # Setup / General Deployment <-

* Multipass / Terraform
    * Deploys instances
    * Creates Ansible inventory
    * Modifies local hosts file

Playbook run took 0 days, 0 hours, 2 minutes, 38 seconds

* General server configuration
    * apt packages
    * hashicorp repository
    * docker (clients)
    * dnsmasq
    * pip + some packages
    * tools that should be standard
      * atop, jq, lynx, tree, etc

Playbook run took 0 days, 0 hours, 5 minutes, 7 seconds

-------------------------------------------------

-> # Setup / PKI <-

* Creates a self-signed Certificate Authority
* Distributes the CA certificate to servers and clients
  * Places the CA certificate in the trusted store
* Creates a certificate for our web app

Playbook run took 0 days, 0 hours, 0 minutes, 27 seconds

-------------------------------------------------

-> # Setup / Consul <-

* Creates a Consul CA, server and client certificates
* Creates an encryption key
* Consul is bootstrapped - token is saved on workstation
* Several Consul policies are created
* Default Consul policy is modified
  * To allow DNS lookups for dnsmasq
* CNI (Container Network Interface) plugin is installed

Playbook run took 0 days, 0 hours, 1 minutes, 2 seconds

-------------------------------------------------

-> # Setup / Vault <-

* Creates a TLS certificate for the Vault nodes
  * Signed by our private CA
* Uses Consul as storage backend
  * Creates Consul ACL tokens for Vault
* Initializes Vault on server1
* Unseals the Vault
* Creates admin policy
* Creates admin user - password is saved on workstation
* Enables kv/2 secrets engine
* Revokes initial root token
* Enables logrotate for Vault
* Enables auditing to file

Playbook run took 0 days, 0 hours, 0 minutes, 36 seconds

-------------------------------------------------

-> # Setup / Nomad <-

* Creates a Nomad policy in Consul
* Creates Consul ACL tokens for Nomad servers and clients
* Nomad is bootstrapped - token is saved on workstation
* Nomad token for operator is created

Playbook run took 0 days, 0 hours, 0 minutes, 52 seconds

-------------------------------------------------

-> # Setup / Nomad + Vault integration && Nomad demo jobs <-

* Nomad / Vault integration
  * Creates a Vault policy for the demo apps
  * Creates a Nomad server role in Vault
  * Places the web app certificate in Vault

Playbook run took 0 days, 0 hours, 0 minutes, 11 seconds

* Demo jobs
  * Starts Traefik
  * Starts AT-Demo

Playbook run took 0 days, 0 hours, 0 minutes, 6 seconds

-------------------------------------------------

-> # Setup / Demo / Traefik <-

* Traefik is registered within Consul
* Retrieves TLS certificates from Vault

-------------------------------------------------

-> # Setup / Demo / Web App <-

* Pulls a container image
* Registers itself within Consul
* Registers itself within Traefik through tags

-------------------------------------------------

-> return 0 <-

-------------------------------------------------

-> # Resources <-



-> [Repo](https://github.com/chrisvanmeer/at-hashi-demo) <-
-> [Presentation](https://github.com/chrisvanmeer/hashitalks-2022-benelux)

-------------------------------------------------

-> # Contact <-

Email          [c.v.meer@atcomputing.nl](mailto:c.v.meer@atcomputing.nl)
Website        [chrisvanmeer.nl](https://chrisvanmeer.nl)
GitHub         [@chrisvanmeer](https://github.com/chrisvanmeer)
LinkedIn       [chrisvanmeer](https://linkedin.com/in/chrisvanmeer)
Reddit         [u/chrisvanmeer](https://www.reddit.com/user/chrisvanmeer)
               [r/hashicorp](https://www.reddit.com/r/hashicorp)
               [r/consul](https://www.reddit.com/r/consul)
Discord        [The DevOps Lounge](https://discord.gg/devopslounge)
Meetup         [Amsterdam HashiCorp User Group](https://www.meetup.com/amsterdam-hashicorp-user-group)

