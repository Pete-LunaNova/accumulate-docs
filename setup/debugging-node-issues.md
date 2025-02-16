# Debugging node issues

### The node is not responding to API requests

1. Run `netstat -alpn | grep <port>` to check if Accumulate is or is not listening on the relevant port. A response like `tcp6 0 0 :::16695 :::* LISTEN 20355/accumulated` indicates that Accumulate **is** listening.
   * If Accumulate is listening, something is blocking or interfering with connections to the node. If you can connect to any port (including SSH or HTTPS), the issue is likely an incorrect firewall configuration.
   * Otherwise (if Accumulate is not listening),
2. Check if Tendermint is still catching up. Open `http://<your-node>:<tendermint-rpc>/status` in your browser, or make the equivalent RPC call.
   * If you get no response, use `netstat` to check if its listening. If it is listening, see above.
   * If it is not listening, wait for a minute to ensure the node has booted. If there's still no response, ask for help.
   * If you get a response and `catching_up` is `true`, wait for it to finish catching up.
   * If you get a response and `catching_up` is `false`, ask for help.
