dynatrace-ansible-metrics-role
=========

This role enables you to send metrics about Ansible (Tower) job/playbook execution to Dynatrace.  Add the role as tasks within your playbook and specify the metric group and metric name as variables.  Use this to monitor Ansible job executions, failures, changes, deployments, and more within Dynatrace.  For additional monitoring of Ansible, check out the [Ansible Tower Metrics Parser](https://github.com/barrebre/goScrapeAnsibleMetrics), which can be used to send more metrics to Dynatrace.

Requirements
------------

* Works on Linux and Windows target hosts.
* Requires only the (native) uri or win_uri modules.
* [Dynatrace OneAgent](https://www.dynatrace.com/support/help/shortlink/release_notes#oneagent) v1.201+
* [OneAgent metric API](https://www.dynatrace.com/support/help/shortlink/local-api) enabled on target hosts.

Role Variables
--------------

### dynatrace (dt) variables
* dt_metrics_ingest_url: http://localhost:14499/metrics/ingest -> http endpoint for OneAgent metric API
* dt_metrics_group: default -> metric group (ansible.group-name.metric-name) [see restrictions](https://www.dynatrace.com/support/help/shortlink/metric-ingestion-protocol#metric-key-required)
* dt_metrics_name: default -> metric name (ansible.group-name.metric-name) [see restrictions](https://www.dynatrace.com/support/help/shortlink/metric-ingestion-protocol#metric-key-required)
* dt_metrics_value: 1 -> metric value [see restrictions](https://www.dynatrace.com/support/help/shortlink/metric-ingestion-protocol#payload-required)
### ansible (awx) variables
* awx_job_type: default -> the type of job (i.e. deployment, change, configuration, patching, etc) used for reporting
* awx_job_id: 0 -> the id of the job (auto-populated when using Ansible Tower)
* awx_job_template: default -> the job template (auto-populated when using Ansible Tower)
* awx_job_launch_type: default -> the method in which the job was launched (auto-populated when using Ansible Tower)

Dependencies
------------

No external role dependencies

Example Playbook
----------------
```yaml
 name: test ansible metrics # playbook name
 hosts: localhost # target hosts
 tasks: # playbook tasks
   -
    name: my task name # task name
    include_role:
      name: dynatrace-ansible-metrics-role # name of included role
    vars: # variables to pass
      dt_metrics_group: my-group # name of metric group
      dt_metrics_name: jobs.started # name of metric
      dt_metrics_value: 5 # value of metric
```

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
