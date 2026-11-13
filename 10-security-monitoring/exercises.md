# លំហាត់មេរៀនទី ១០៖ Security និង Monitoring

លំហាត់នេះប្រើតែការពិនិត្យ read-only។ កុំកែ firewall, users, SSH config ឬ system services។

## ផ្នែក A៖ សំណួរ

1. Least privilege មានន័យដូចម្តេច?
2. ហេតុអ្វី listening port មិនបញ្ជាក់ថា service អាចចូលពី Internet?
3. តើ logs ត្រូវលាក់ព័ត៌មានអ្វីខ្លះមុនចែករំលែក?
4. ហេតុអ្វីត្រូវមាន tested backup?
5. តើតម្លៃ memory ឬ load តែមួយអាចបញ្ជាក់ថាម៉ាស៊ីនខូចបានទេ?

## ផ្នែក B៖ Read-only checks

~~~bash
whoami
id
ls -ld "$HOME"
uptime
free -h
df -h
ss -tuln
~~~

បើ systemd មាន៖

~~~bash
systemctl --type=service --state=running
journalctl -p warning -b -n 30
~~~

កត់ត្រា observation មួយដែលអ្នកចង់ស៊ើបអង្កេតបន្ថែម និងព័ត៌មាន context ដែលខ្វះ។

## លក្ខខណ្ឌបញ្ចប់

- អាចរៀបរាប់ basic security practices។
- អាចសរសេរ monitoring note ដោយមិនបង្ហាញ sensitive data។
- មិនបិទ firewall ឬកែ remote access settings ក្នុងលំហាត់។
