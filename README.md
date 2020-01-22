# Aries Cloud Agent - Python (ACA-py) Demo Controllers

Web controllers for the [Aries Cloud Agent - Python (ACA-Py)](https://github.com/hyperledger/aries-cloudagent-python) Faber/Alice agent [demo](https://github.com/hyperledger/aries-cloudagent-python/tree/master/demo#the-alicefaber-python-demo) aimed primarily at business or first-time Aries developers. The controllers are deisgned to provide an easy-to-use interface to showcase agent-to-agent interactions.

_See [Note to Developers](#note-to-developers) if you are a developer looking for specific information about the demo controller codebases._

## Table of Contents

- [Running With Docker](#running-with-docker)
- [Running Locally](#running-locally)
    - [Prerequisites](#prerequisites)
        - [VON Network](#von-network)
        - [ACA-Py Agents](#aca-py-agents)
    - [Running Controllers](#running-controllers)
- [Demo Walkthrough](#demo-walkthrough)
    1. [Alice graduates from Faber College](#1-alice-graduates-from-faber-college)
    2. [Alice accepts an invitation from Faber for her Degree](#2-alice-accepts-an-invitation-from-faber-for-her-degree)
    3. [Faber issues a Degree credential to Alice](#3-faber-issues-a-degree-credential-to-alice)
    4. [Alice applies for a job at Acme](#4-alice-applies-for-a-job-at-acme)
    5. [Acme agrees to interview Alice](#5-acme-agrees-to-interview-alice)
    6. [Acme requests a proof of education from Alice](#6-acme-requests-a-proof-of-education-from-alice)
- [Note to Developers](#note-to-developers)

### Running With Docker

This will be the easiest setup option. Please see the [Docker Web Demo](./demo/README_web.md) documentation for instructions.

### Running Locally

#### Prerequesites

##### VON Network

The demos require a Hyperledger Indy Node network. Is is recommended to use the [VON Network](https://github.com/bcgov/von-network), developed as a portable Indy Node Network implementation for local development. Instructions for setting up the `von-network` can be viewed [here](https://github.com/bcgov/von-network#running-the-network-locally) or [here](./demo/README_web.md#von-network).

**Note: the demos will not work without a local VON Network running.**

##### ACA-Py Agents

Controllers are dependent on their respective cloud agents. Please follow instructions for [running agents locally](https://github.com/hyperledger/aries-cloudagent-python/tree/master/demo#running-locally) or [running agents in docker](https://github.com/hyperledger/aries-cloudagent-python/tree/master/demo#running-in-docker) as controllers wont do anything if agents are not running.

**Note: the controllers will not do anything without running their agents.**

#### Running Controllers

Please see the [Controller](./demo/controllers/README.md) documentation for instructions on how to run controllers in your local environment.

### Demo Walkthrough

If you have made it this far, congratulations! 🎉 You are well on your way to becoming an Aries expert 💪.

You should have the controllers open in three different tabs of your browser:
- Faber at http://localhost:9021 (running with docker) or http://localhost:5001 (running locally)
- Alice at http://localhost:9031 (running with docker) or http://localhost:4200 (running locally)
- Acme at http://localhost:9041 (running with docker) or http://localhost:3000 (running locally)

**Scenario:**

Alice 👩 is a former student of Faber College ("Knowledge is Good") 🎓and wants to work for the coveted startup, Acme 🚀. The job Alice is looking to land requires a college diploma. Alice will connect with Faber to obtain her degree and then provide proof of her education to Acme in order to land her dream job.

**Steps:**

This part will take you through the specific steps of the Faber-Alice-Acme workflow. Faber, Alice and Acme are each tailored to perform specific functions, as you will see. Throughout every interaction keep in mind that the agents are doing all the work behind the scenes. The controllers are interacting through an API with the agents.

#### 1. Alice graduates from Faber College
_What an auspicious day! The many sleepless nights are over. Alice made it through her program of study and is on her way to a successful career. Faber offers all of their alumni to stay connected by extending an invitation code to all graduating students._

In the Faber browser tab, the home screen should display 4 options to choose from. The `Connections` page is where Faber can view, issue invitations and accept connections.

Navigate to the `New` tab where you will see a button to `Create a New Invitation`. Upon clicking that you will see a JSON invitation object and an invitation URL (which is an encoded version of invitation object). Notice the different fields in the invitation object.

Copy either the invitation object or the URL (there is a handy copy button to the right of each of the fields). You will pass the invitation over to Alice.

_Aside: If you navigate to the `Pending` tab you will see a new invitation card with a connection ID and a timestamp for when the invitation was created. This is a handy way to determine whether an invitee has accepted an invitation request or not._

#### 2. Alice accepts an invitation from Faber for her Degree

_Alice connects to her former college and requests a copy of her degree to keep in a digital wallet stored on her phone._

Open the Alice browser tab, and on the home screen you will see 3 options to choose from. The `Connections` page is where Alice will accept her invitation from Faber. Notice that Alice has the same connection tabs as Faber does.

Navigate to the `Accept` tab where you will see the option to either paste the invitation object or the invitation URL (depending on which one you copied). If you are successful the `Accept Invitation` button will activate. Press it.

Navigate over to the `Active` tab to see a connection to Faber. Similary, Faber's  `Active` connections tab will show a connection to Alice.

#### 3. Faber issues a Degree credential to Alice

In the home screen of Faber you will see options for `Credential Schemas` and `Credential Definitions`. When the Faber agent was started, a degree schema and corresponding credential definition was issued to the VON Network. It is from these that Faber can construct a degree credential to deliver to Alice via their peer-to-peer (P2P) connection.

Navigate to the `Credential Schemas` page and select a schema from the select input. Notice the structure of the schema and the attributes including the `attrNames` list of credential attributes. Navigate over the the `Credential Definitions` page and select a credential definition from the drop down. Notice the difference in structure from the schema.

Navigate now to the `Credentials` page. This is where Faber can issue a credential to a connection. You will need to select a `Connection`, `Credential Schema` and a `Credential Definition` from the select inputs. In this case Alice is the only connection and a degree is the only credential that Faber can issue.

_Aside: Feel free to adjust the credential attributes but make sure they conform to valid JSON array structure otherwise the agent will fail to issue the credential._

When you are ready to issue the credential to Alice press the `Send Credential` button.

Open the Alice browser tab. In the home screen you will see a `Credentials` option. If Alice successfully received the degree credential from Faber, you will see it here. Notice the different attributes displayed in the credential.

#### 4. Alice applies for a job at Acme
_Alice is super excited to apply for her job. She sends an invitation request to Acme._

See if you can follow the same approcah above to connect Faber to Alice. In this case Alice will create a new invitation.

#### 5. Acme agrees to interview Alice
_Acme agrees to connect with Alice._

See if you can follow the same approcah above to connect Faber to Alice. In this case, Acme will accept the invitation. Acme has all of the same options in its `Connection` page as Faber and Alice.

If you are successful Alice and Acme will have active connections with eachother.

#### 6. Acme requests a proof of education from Alice
_Acme was floored by Alice's resume and interview. They just need her to show a proof of her education (for HR purposes) and they will offer her a job._

Open the Acme browser tab. In the home screen you will see a `Proof Requests` option. Navigate to the `Request Proof` tab. Acme can request a proof from any of their connections. Select the Alice connection. For the Credential Definition ID, you will need to open the Faber browser tab and navigate to the `Credential Definitions` page. Select the credential definition from the list you are interested in receiving a proof for. You will need to copy the `id` which will look something along the lines of

```
vDdXBfpoDSCwTHqwH83AZ:3:CL:138:default
```
_Note: yours will have different numbers and letters but should be structured the same._

Now navigate back to Acme's `Request Proof` page and paste the ID in the `Credential Definition ID` input. Press the `Request Proof` button.

In the `Proofs` page of Acme you will see a new proof request sent (Alice can correspondingly see all proofs requested in her `Proofs` page). If the credential was successfully verified you will see a checkmark appear in Acme's proof request, indicating that Alice did successfully prove her education from Faber.

_Note: You will have to refresh the screen to see the verified proof._

Congratulations! You have finished the Faber-Alice-Acme demo. This is a good chance to dive into the agents to understand what's going on behind the scenes of all of these interactions. Feel free to also browse through the controller code and see where the controllers handle requests and responses between themselves and the agents.

### Note to Developers

Each controller used in the demo is built with a different web framework, which is intended to further demonstrate the versatility of agents. Controllers can be built using any web or mobile framework/technology of your choosing.

If you are interested in studying/extending the [Faber](./demo/controllers/faber-controller/README.md), [Alice](/demo/controllers/alice-controller/README.md) or [Acme](/demo/controllers/acme-controller/README.md) controller codebases, each controller contains documentation with specific implementation details and how-tos for setting up development and debugging environments.