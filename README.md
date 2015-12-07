Got Your Back
=============

Got Your Back (GYB) is a command line tool for backing up your Gmail messages to your local computer. It uses the standard IMAP protocol but also takes advantage of some custom Gmail IMAP extensions.

Learn more about how GYB works with the [Getting Started Guide](https://github.com/jay0lee/got-your-back/wiki).

Download the latest GYB version from the [Releases Page](https://github.com/jay0lee/got-your-back/releases).

# Local bug fixes

The code in this repo was cloned from the main [got-your-back repo](https://github.com/jay0lee/got-your-back).

To get this to work I needed to fix some bugs. The following were implemented in two commits ([7fa7f74](https://github.com/dfalster/got-your-back/commit/7fa7f74928514239afada197dfc8aed9f3043ac7), [0ae508d](https://github.com/dfalster/got-your-back/commit/0ae508ddde187d522bc2643267077dbea20a4032).

1. On line 1489, commented out doGYBCheckForUpdates()
2. Edited gyb.py, searched for "open(last_update_check_file" (there are 3 of them) and changed the 'rb' to 'r' or 'wb' to 'w'. The file it's trying to use is a text file, not a byte file. [see #57](https://github.com/jay0lee/got-your-back/issues/57)
3. Fixed error with restoring backup to new account [see #51](https://github.com/jay0lee/got-your-back/issues/51)
4. I also added Also added a print message so that I know which email is being loaded, allowing better troubleshooting

In addition you'll need to

1. Run using python3
2. Download [six.py](https://raw.githubusercontent.com/django/django/master/django/utils/six.py
) and save within this repo.

# To run

The instructions below assume you have two address email_old and email_new:

Estimate size of backup

```
python3 docs/got-your-back/gyb.py --email email_old --action estimate
```

Backup email_old, saving data into a folder called GYB-GMail-Backup-email_old

```
python3 docs/got-your-back/gyb.py --email email_old --action backup --local-folder GYB-GMail-Backup-email_old
```

Restore message to new account

```
python3 docs/got-your-back/gyb.py --email email_new --action restore --local-folder GYB-GMail-Backup-email_old
```
