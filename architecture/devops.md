# Devops

- [Devops](#devops)
  - [Devops Roadmap](#devops-roadmap)
  - [Ansible Notes](#ansible-notes)
    - [Terms](#terms)

## Devops Roadmap

- <https://roadmap.sh/devops>
- Also a useful list: <https://www.reddit.com/r/devops/comments/j5k2nw/switching_to_a_career_in_devops_which_tools_will/>
  - Config management; Ansible, Puppet, Chef, Saltstac, Packer (kinda also provisioning)
    Provisioning: Terraform, Salt, Ansible, Cloudformation (terraform the best in class in my opinion)
    CI/CD: Jenkins, Bamboo, GitLab CI/CD, CircleCI, Travis CI, Jfrog Pipelines, TeamCity
    Version Control: Git, SVN
    Container Orchestration: K8s, Nomad, Rancher, Swarm, ECS (k8s commonly considered best in class)
    Monitoring & Alerting: Nagios, Zabbix, Prometheus, New Relic, Datadog
    Cloud Infrastructure: AWS, GCP, Azure
    Load Balancing: ALBs, HAProxy, Nginx
    Scripting/coding: Python, Bash, Groovy, Go

I am sure I missed a lot. But even more importantly in devops are some general practices and mindsets:

    Collaboration with Developers
    Identifying Bottlenecks
    Infrastructure as Code
    Test driven CI/CD
    Agile/Scrum

I would suggest checking out some books such as the Phoenix Project, DevOps Handbook, The Goal, Site Reliability Engineering (O'Reilly), Infrastructure as Code (O'Reilly),


## Ansible Notes

- From linkedIn learning course - <https://www.linkedin.com/learning/learning-ansible-2020/an-introduction-to-ansible?u=75507506>
  - Ansible uses Python & YAML
  - Ansible is Agentless - it uses ssh to push from control node to multiple remote sources.

### Terms

- Control Node/Ansible server - machine with Ansible installed, running ansible scripts which can control/run commands on other machines
- Module: Command or set of similar commands to be executed on the client-side
- Task: Section with a single procedure to be completed
- Role: A way of organizing tasks and related files to be later called in a playbook
- Fact: Information fetched from the client system from the global variables with the gather-facts operation
- Inventory: AKA hosts file - contains information (names/IPs) for ansible client servers
- Play: Execution of a playbook
- Handler: Task which is called only if a notifier is present
- Notifier: Section attributed to a task which calls a handler if the output is changed
- Tag: Name set to a task which can be used later on to issue just that specific task or group of tasks.
