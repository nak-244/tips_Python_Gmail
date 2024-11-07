# Pythonでメールを送る方法

~~~python
import smtplib
from email.mime.text import MIMEText
from email.utils import formatdate

FROM = 'olp.gbp@gmail.com'
PASSWORD = 'dzhaakldxqmcjjdj'
PORT = 587

TO = 'tsuyoshi.nakamura@openloop.co.jp'
BCC = 't23220130n@i.softbank.jp'

SUBJECT = '日本語の題名'
BODY = '''日本語の本文
これは新しい行です
さらに新しい行です'''


def create_msg(from_addr, to_addr, bcc_addr, subject, body):
    msg = MIMEText(body.encode('iso-2022-jp'), 'plain', 'iso-2022-jp')
    msg["From"] = from_addr
    msg['To'] = to_addr
    msg['Bcc'] = bcc_addr
    msg['Subject'] = subject
    msg['Date'] = formatdate()
    return msg


def send_mail(to_addrs, msg):
    smtpobj = smtplib.SMTP('smtp.gmail.com', PORT)
    smtpobj.ehlo()
    smtpobj.starttls()
    smtpobj.ehlo()
    smtpobj.login(FROM, PASSWORD)
    smtpobj.sendmail(FROM, to_addrs, msg.as_string())
    smtpobj.close()


if __name__ == '__main__':
    to_addrs = [TO, BCC]
    msg = create_msg(FROM, TO, BCC, SUBJECT, BODY)
    send_mail(to_addrs, msg)

　~~~
