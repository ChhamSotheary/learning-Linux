# មេរៀនទី ៦៖ Processes, Services និង Logs

## គោលបំណងមេរៀន

- ពន្យល់ process, PID និង background job។
- ពិនិត្យ processes ដោយ ps, top និង pgrep។
- យល់ពី signal និងការបញ្ឈប់ process របស់ខ្លួន។
- ពិនិត្យ service status ដោយ systemd ប្រសិនបើមាន។
- ស្វែងរក logs ដោយ journalctl និង log files។

## ១. Process និង PID

Process គឺជាកម្មវិធីដែលកំពុងដំណើរការ។ ប្រព័ន្ធផ្ដល់ Process ID (PID) ដើម្បីសម្គាល់ process មួយៗ។

~~~bash
ps
ps -ef
top
pgrep -a bash
~~~

- ps បង្ហាញ process ក្នុង context មួយ។
- ps -ef បង្ហាញបញ្ជី process លម្អិតតាម syntax ដែលពេញនិយមលើ Linux។
- top បង្ហាញ process និងការប្រើប្រាស់ធនធានបន្តផ្ទាល់; ចុច q ដើម្បីចេញ។
- pgrep ស្វែងរក process តាមឈ្មោះ pattern; -a រួមបញ្ចូល command line ប្រសិនបើគាំទ្រ។

Option syntax អាចខុសគ្នាតាម implementation; ប្រើ man ps និង man pgrep។

## ២. Foreground និង Background Jobs

Command ដែលរត់ក្នុង terminal ជាទូទៅជា foreground job។ អ្នកអាចដាក់ & នៅចុង command ដើម្បីរត់វាជា background job ក្នុង shell session ដដែល៖

~~~bash
sleep 60 &
jobs
ps -p "$!" -o pid,stat,comm
~~~

$! ជា shell variable ដែលមាន PID របស់ background command ចុងក្រោយ។ កុំសន្មតថា PID មួយនឹងនៅដដែល; process អាចបញ្ចប់មុនពេលអ្នកពិនិត្យ។

## ៣. Signals និងការបញ្ឈប់ Process

Signals ជាវិធីស្នើសុំឱ្យ process ធ្វើសកម្មភាពមួយ។ Ctrl+C ជាទូទៅផ្ញើ SIGINT ទៅ foreground process។ kill command ផ្ញើ signal ទៅ PID៖

~~~bash
kill -TERM "$!"
~~~

SIGTERM ស្នើឱ្យ process បញ្ចប់ដោយសុវត្ថិភាព។ SIGKILL (kill -9) បង្ខំបញ្ចប់ ហើយគួរប្រើតែជាជម្រើសចុងក្រោយ ព្រោះកម្មវិធីមិនមានឱកាសសម្អាតធនធាន។ ក្នុងមេរៀននេះ ប្រើ kill តែលើ sleep process ដែលអ្នកបង្កើតផ្ទាល់។ កុំសម្លាប់ process ប្រព័ន្ធ ឬ process របស់អ្នកដទៃ។

## ៤. Services និង systemd

Service ជា process/background function ដែលគ្រប់គ្រងដោយ service manager។ Linux distributions ជាច្រើនប្រើ systemd ប៉ុន្តែមិនមែនគ្រប់ប្រព័ន្ធទាំងអស់ទេ។

ពិនិត្យថាមាន systemd៖

~~~bash
systemctl --version
~~~

បើប្រព័ន្ធប្រើ systemd អាចពិនិត្យ service ដោយមិនផ្លាស់ប្ដូរស្ថានភាព៖

~~~bash
systemctl status
systemctl list-units --type=service --state=running
systemctl status ssh
~~~

ឈ្មោះ service ខុសគ្នាតាម distribution; នៅ Ubuntu អាចប្រើ ssh ខណៈ Fedora ជាទូទៅប្រើ sshd។ បើ service មិនមាន ឬមិនអនុញ្ញាតឱ្យមើល status ក៏មិនមានន័យថាប្រព័ន្ធខូចទេ។

Restart, stop, disable ឬ enable service ជាសកម្មភាពប្ដូរប្រព័ន្ធ។ កុំធ្វើលើ service សំខាន់ដោយគ្មានគោលបំណង និងសិទ្ធិច្បាស់។

## ៥. Logs និង journalctl

Logs ជាកំណត់ត្រាព្រឹត្តិការណ៍សម្រាប់ជួយ troubleshooting។ លើ systemd systems អាចប្រើ៖

~~~bash
journalctl -b -n 30
journalctl -p warning -b
journalctl -u ssh --since today
~~~

- -b កំណត់ទៅ current boot។
- -n កំណត់ចំនួនបន្ទាត់ចុងក្រោយ។
- -p កំណត់ priority។
- -u ច្រោះតាម service។

ការចូល logs អាចមានកម្រិត permissions ហើយ logs អាចមាន username, IP ឬព័ត៌មានសំខាន់។ កុំបង្ហោះ logs ទៅសាធារណៈដោយមិនពិនិត្យ/លុប sensitive data។

ប្រព័ន្ធខ្លះរក្សា logs ក្នុង /var/log ដូចជា /var/log/syslog ឬ /var/log/messages។ ឈ្មោះ និងរបៀប logging អាស្រ័យលើ distribution និង configuration។

## ៦. Troubleshooting Flow

ពេល service មានបញ្ហា៖

1. សម្គាល់អ្វីដែលមិនដំណើរការ និងពេលចាប់ផ្ដើម។
2. ពិនិត្យ service status និង exit/error message។
3. ពិនិត្យ logs ជុំវិញពេលកើតហេតុ។
4. ពិនិត្យ resources និង dependencies។
5. កត់ត្រាការផ្លាស់ប្ដូរថ្មីៗ។
6. ធ្វើ action តូចបំផុតដែលអាចសាកល្បងបាន។
7. ផ្ទៀងផ្ទាត់លទ្ធផល និង rollback ប្រសិនបើបញ្ហាកាន់តែធ្ងន់។

កុំចាប់ផ្ដើមដោយ restart service ទាំងអស់ ឬលុប logs ព្រោះវាអាចលាក់មូលហេតុដើម។

## ៧. កិច្ចការអនុវត្ត

1. រត់ ps -ef និងស្វែងរក shell របស់អ្នក។
2. រត់ top រយៈពេលខ្លី ហើយចេញដោយ q។
3. បង្កើត background job ដោយ sleep 60 &។
4. ប្រើ jobs និង ps -p "$!" ដើម្បីមើលវា។
5. បញ្ឈប់តែ process sleep ដែលអ្នកបានបង្កើត ដោយ kill -TERM "$!"។
6. បើមាន systemd សូមពិនិត្យ service status មួយដោយមិន restart។
7. មើល journal entries ចុងក្រោយ បើ permission អនុញ្ញាត ហើយកុំចែករំលែក logs ដែលមានព័ត៌មានរសើប។

## សង្ខេប

Process មាន PID ហើយអាចពិនិត្យដោយ ps/top/pgrep។ Background jobs ក្នុង shell អាចគ្រប់គ្រងដោយ jobs និង $!។ Signals ស្នើសុំឱ្យ process បញ្ចប់។ systemctl ពិនិត្យ/គ្រប់គ្រង services លើ systemd។ journalctl ជួយអាន logs តាម boot, priority និង service។

## ឯកសារយោង

- [Linux ps manual](https://man7.org/linux/man-pages/man1/ps.1.html)
- [Linux kill manual](https://man7.org/linux/man-pages/man1/kill.1.html)
- [systemctl manual](https://www.freedesktop.org/software/systemd/man/latest/systemctl.html)
- [journalctl manual](https://www.freedesktop.org/software/systemd/man/latest/journalctl.html)
