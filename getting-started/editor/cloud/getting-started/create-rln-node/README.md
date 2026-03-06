# Create RLN Node

{% stepper %}
{% step %}
### Initiate RLN Node Creation

* Navigate to the `/nodes` page. Here you'll see an overview of your current nodes and the option to create new ones.

![](<../../../../../.gitbook/assets/image (5)>)

* Click the "Create Node" button. This redirects you to a page where you can begin the node creation process.
{% endstep %}

{% step %}
### Configure Your RLN Node

* On the redirected page, fill out the node creation form by entering a unique name for your new node. This name helps you identify the node in your dashboard.
* After entering a name, click the "Create" button to submit the form and start the node creation process.

![](<../../../../../.gitbook/assets/image (6)>)

{% hint style="info" %}
On the Regtest Network, block mining doesn’t happen automatically. Manually mine blocks using the provided curl commands whenever you want the chain to advance or confirm activity.

To mine blocks:

```bash
curl --location 'http://18.119.98.232:5000/execute' \
  --header 'Content-Type: application/json' \
  --data '{ "args": "mine 10" }'
```

If you need test BTC, use the `sendtoaddress` command (acts like a local faucet), then manually mine a block with the curl command above to confirm it:

```bash
curl --location 'http://18.119.98.232:5000/execute' \
  --header 'Content-Type: application/json' \
  --data '{ "args": "sendtoaddress <address> 0.1" }'
```
{% endhint %}
{% endstep %}

{% step %}
### Monitor Node Creation Status

* After submitting the form, a new item is added to the nodes table on the `/nodes` page. Initially it will display a status of IN\_PROGRESS while the node is being built. During this phase you cannot perform operations with the node.
* You can view detailed information by visiting `/nodes/{nodeId}`. That page shows current status, build progress, endpoint details, and other configurable options so you can monitor the node’s setup process.

![](<../../../../../.gitbook/assets/image (7)>)

#### Understanding statuses

* IN\_PROGRESS: Node is under construction. No interactions can be made.
* RUNNING: Node has been successfully built and is fully operational.
{% endstep %}

{% step %}
### Final Verification

* Once the status changes to RUNNING, verify the node appears correctly in your dashboard and that you can access its features and settings.

![](<../../../../../.gitbook/assets/image (8)>)
{% endstep %}
{% endstepper %}
