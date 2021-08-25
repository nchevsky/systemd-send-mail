# Usage
1. Install to `/etc/systemd/system`:
   - `send-mail@.service`: systemd unit
   - `send-mail`: Script invoked by `send-mail@.service` to send an e-mail
2. Optionally configure recipient's and sender's e-mail addresses in `send-mail`:

   ```
   RECIPIENT=jdoe@example.com
   SENDER=jschmoe@example.com
   ```
   These default to `root@<hostname>` and `<failed-unit-user>@<hostname>`.
3. Add to the unit(s) of whose failures you would like to be notified:

   ```
   [Unit]
   ...
   OnFailure=send-mail@%N.service
   ...
   ```
4. Reload the modified unit(s):
   ```
   $ sudo systemctl daemon-reload
   ```
