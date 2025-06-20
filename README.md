# Logwatch Automation Script for Cybersecurity Monitoring

This repository contains a shell script that automates and enhances **Logwatch**, a log analyzer for Linux systems, for use in **SOC operations, compliance reporting, and system administration**.

---

## Features

- Automatic installation of Logwatch and PDF tools
- Custom SOC-branded HTML reports
- Predefined modes: `daily-report`, `weekly-report`, `monthly-report`
- Email-ready outputs with PDF attachments
- Audit-friendly reporting for ISO 27001, SOC2, PCI-DSS, etc.

---

## Quick Start

### 1. Clone the Repo
```bash
git clone https://github.com/yourusername/logwatch-automation.git
cd logwatch-automation
```

### 2. Make Script Executable
```bash
chmod +x logwatch.sh
```

### 3. Install Dependencies & Set Up Logwatch
```bash
./logwatch.sh install
```

---

## Usage

### Daily Report
```bash
./logwatch.sh daily-report
```

### Weekly Report (Auto PDF)
```bash
./logwatch.sh weekly-report --auto-pdf
```

### Email Report (High Detail)
```bash
./logwatch.sh run --range yesterday --detail High --output mail --mailto soc@example.com
```

---

## Email Configuration

To use the `--mailto` feature, configure an SMTP client (like `ssmtp` or `postfix`) on your Linux server.

### Option A: Using `ssmtp`
```bash
sudo apt install ssmtp
sudo nano /etc/ssmtp/ssmtp.conf
```
Example config:
```ini
root=you@example.com
mailhub=smtp.yourprovider.com:587
AuthUser=you@example.com
AuthPass=yourpassword
UseSTARTTLS=YES
```

### Option B: Using `postfix`
```bash
sudo apt install postfix
sudo nano /etc/postfix/main.cf
```

Add the following:
```ini
relayhost = [smtp.yourprovider.com]:587
smtp_sasl_auth_enable = yes
smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd
smtp_use_tls = yes
```

---

## Customizing Logwatch Reports

To modify specific service parsing (like `sshd`, `audit`, or `sudo`):

```bash
sudo mkdir -p /etc/logwatch/conf/services/
sudo cp /usr/share/logwatch/default.conf/services/sshd.conf /etc/logwatch/conf/services/
sudo nano /etc/logwatch/conf/services/sshd.conf
```

Adjust regex or detail level as needed.

---

## Directory Structure Example
```bash
/var/reports/logwatch/
├── daily_2025-06-20.pdf
├── weekly_2025-06-16.pdf
└── logwatch_2025-06-19.html
```

---

## License

MIT License

---

## Maintained By

- Author: Yash Patel
- Blog: [Medium Post](https://medium.com/your-logwatch-automation-guide)

---

Feel free to fork, enhance, or submit pull requests!

Happy Monitoring!
