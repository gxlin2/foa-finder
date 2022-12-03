
# My Changes:
`requirements.txt` from the original repo refused to work for me on Oracle Linux or Ubuntu Server 22.04. I've refined it by removing version requirements for certain dependencies. Hasn't broken for me yet, feel free to create an issue ticket if it does for you. 

Documentation has been streamlined and improved for more concise instructions.

`app.py` from the original repo, for some reason, commented out the `send_to_slack(slack_text)` line required for sending the message to Slack. That's been uncommented.

Also have removed `nonkeywords.csv`. I don't think it provides a very meaningful contribution to the code.
# Installation and Setup Instructions
**Tested on Ubuntu 22.04**
1. Install the latest version of Python and `pip`. 
2. Clone this repository (`git clone https://github.com/AGaiki/foa-finder.git`)
3. Navigate into the folder and execute `pip install -r requirements.txt` (sometimes you might need `pip3` depending on if you have an existing version of Python; Additionally, while this might not be the best practice, you might need to prepend that with `sudo` if it complains about not being able to access or write to a specific directory, although running that in an environment will probably solve that).
4. Create your Slack app: https://api.slack.com/apps
5. Navigate to the `Incoming Webhooks` page from the sidebar.
6. Activate the switch for Incoming Webhooks and create a new Webhook. Note the URL, you will need it for the next steps. You will also need to invite it to a Slack instance.
7. Using your CLI text editor of choice, open `/etc/environment` and add a new line like so: `SLACK_WEBHOOK_URL="SlackURL"`, replacing `SlackURL` with the webhook link.
8. Edit `keywords.csv` to include whatever values you wish. I haven't changed the original repo owner's keywords, so make sure to remove and add whatever you wish in the same format as it. While, yes, csv does stand for "comma separated values," there are no commas in that document. That is by design.
9. Finally, run `python app.py` (or `python3 app.py` if there are multiple versions of Python installed).
10. Profit! 
## Level 2: Cronjobs
Modeling after the existing documentation from the original repo, I have set up cron jobs for 6:00PM daily:
1. Run `crontab -e` on the CLI. It might ask you to pick a text editor.
2. Create a new line. In my case, I'd be inputting the following lines: `0 18 * * 1-7 python3 ~/foa-finder/app.py`. For help creating valid crontab syntax, please refer to this excellent tool: https://crontab.guru/#0_18_*_*_1-7. 
3. Save.
4. Profit!
