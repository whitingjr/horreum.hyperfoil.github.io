# Create a Test and upload a Run

This tutorial will present the most basic thing Horreum can do: store your benchmark results in the form of JSON files. We assume that you already went through the [previous tutorial](start.html), Horreum is up and you are logged in.

<div class="screenshot"><img src="/assets/images/create_test/01_logged_in.png"></div>

Press the **New Test** button and fill the test name. Test names must be unique within Horreum.

<div class="screenshot"><img src="/assets/images/create_test/02_new_test.png" /></div>

Click on **Save** button on left side at the bottom - a blue banner will confirm that the test was created.

Now we can prepare the JSON document representing our benchmark results - open `/tmp/run.json` with your favorite text editor and paste in this:

```json
{
  "$schema": "urn:my-schema:1.0",
  "throughput": 1234.5
}
```

Now copy and paste this into shell; the reply will be just `1` - the ID of the newly uploaded run.

```bash
TOKEN=$(curl -s http://localhost:8180/realms/horreum/protocol/openid-connect/token \
    -d 'username=user' -d 'password=secret' \
    -d 'grant_type=password' -d 'client_id=horreum-ui' \
    | jq -r .access_token)
TEST='Foobar'
START='2021-08-01T10:35:22.00Z'
STOP='2021-08-01T10:40:28.00Z'
OWNER='dev-team'
ACCESS='PUBLIC'
curl 'http://localhost:8080/api/run/data?test='$TEST'&start='$START'&stop='$STOP'&owner='$OWNER'&access='$ACCESS \
    -s -H 'content-type: application/json' -H 'Authorization: Bearer '$TOKEN \
    -d @/tmp/run.json
```

Let's navigate into the tests overview (main page) by clicking the **Tests** link in the main menu on the top left of the page:

<div class="screenshot"><img src="/assets/images/upload/00_tests.png" /></div>

Click on the run count number with open-folder icon to see the listing of all runs for given test:

<div class="screenshot"><img src="/assets/images/upload/01_runs.png" /></div>

At this point don't worry about the 'No schema' warning. Hit the run ID with arrow icon in one of the first columns and see the contents of the run you just created:

<div class="screenshot"><img src="/assets/images/tutorial/uploaded_run.png" /></div>
