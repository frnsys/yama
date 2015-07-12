# Yama

Processes are registered and deregistered with Yama. Yama can audit running processes to check that registered processes are still running. If they are not, an email is sent for each missing process.

## Installation

    pip install yama

## Config

Yama looks for its configuration file in `~/.yama`, in the yaml form of:

    mailer:
        host: smtp.gmail.com
        port: 587
        user: some-email@gmail.com
        password: some-password
        admins:
            - some-admin@gmail.com

This configures the email that Yama sends emails from.

## Usage

From within python scripts, you can register and deregister the script's process like so:

    import yama

    pid = yama.pid()
    yama.register(pid)

    # do stuff

    yama.deregister(pid)

Or, more conveniently, you can wrap Yama around any command, e.g.:

    yama run python my_script.py

Then you can audit running processes with the command:

    yama audit

Or, from within a python script, as:

    yama.audit()

You might want to setup Yama as a cron job to regularly audit:

    crontab -e

    # Audit every 2 min
    */2 * * * * yama audit

## More details

Yama stores its register in `/tmp/yama`. On reboot, all processes get killed, and this file gets erased, so the register is wiped clean.

## The name

Yama is the God of Death in Hinduism and Buddhism. In _Journey to the West_, Yama has magistrates and clerks who manage registers of how long certain creatures live and when they are due to die.