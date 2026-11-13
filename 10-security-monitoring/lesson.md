# មេរៀនទី ១០៖ Linux Security និង Monitoring

## គោលបំណង

- អនុវត្ត least privilege, updates និង secure account habits។
- ពិនិត្យ permissions, listening ports និង service state។
- មើល resource usage និង logs។
- បង្កើត checklist សម្រាប់ monitoring និង incident notes។
- ជៀសវាងការប្ដូរ security controls ដោយគ្មានផែនការ។

## ១. មូលដ្ឋានសុវត្ថិភាព

- ប្រើ user ធម្មតាសម្រាប់ការងារប្រចាំថ្ងៃ។
- ប្រើ sudo តែសម្រាប់កិច្ចការដែលត្រូវការសិទ្ធិខ្ពស់ និងយល់ command។
- ដំឡើង updates ពី trusted repositories តាម maintenance window។
- កំណត់ permissions តាម least privilege។
- ប្រើ password/SSH key management ដែលមានសុវត្ថិភាព និងកុំចែករំលែក private keys។
- បិទ services ដែលមិនចាំបាច់ តែធ្វើតាម change process និងចេះ rollback។
- មាន tested backups និងកំណត់ recovery objectives។
- រក្សា security logs ដោយកំណត់ការចូលប្រើ និង retention។

## ២. ពិនិត្យ User និង File Permissions

~~~bash
whoami
id
sudo -l
ls -ld "$HOME"
~~~

sudo -l បង្ហាញ commands ដែល user អាចអនុវត្តតាម sudo policy។ កុំរត់ sudo command តាមបញ្ជីនេះ ប្រសិនបើមិនមានគោលបំណងច្បាស់។ កុំបង្ហោះ output ដែលអាចបង្ហាញ user/group names ឬ system details ទៅសាធារណៈដោយមិនពិនិត្យ។

## ៣. ពិនិត្យ Services និង Listening Ports

~~~bash
systemctl --type=service --state=running
ss -tuln
~~~

ពិនិត្យថា services/ports ណាខ្លះត្រូវការសម្រាប់ប្រព័ន្ធ។ Listening socket មិនបញ្ជាក់ exposure ទៅ Internet ទេ; ពិនិត្យ bind address, firewall, routing និង cloud/security group rules ផងដែរ។

Firewall tools ដូចជា UFW និង firewalld មាន command/status ខុសគ្នាតាម distro។ ប្រើ status/read commands ដើម្បីសង្កេតមុន។ កុំបិទ firewall ដើម្បីដោះស្រាយ connection issue។

## ៤. Monitoring Resources

~~~bash
uptime
free -h
df -h
top
~~~

- uptime បង្ហាញ uptime និង load averages។
- free -h បង្ហាញ memory/swap summary។
- df -h បង្ហាញ filesystem usage។
- top បង្ហាញ process និង resource activity; ចុច q ដើម្បីចេញ។

តម្លៃមួយមុខមិនគ្រប់គ្រាន់ដើម្បីសន្និដ្ឋានថាប្រព័ន្ធមានបញ្ហាទេ។ ប្រៀបធៀបជាមួយ baseline, workload និងពេលវេលា។

## ៥. Logs និង Incident Notes

ប្រើ journalctl ឬ distro log locations ដើម្បីពិនិត្យ errors ជុំវិញពេលកើតហេតុ៖

~~~bash
journalctl -p warning -b -n 50
~~~

កុំកែ ឬលុប logs ដើម្បីលាក់សកម្មភាព។ កត់ត្រា៖ ពេលវេលា, service, error text, impact, changes ថ្មីៗ និងជំហានដែលបានសាក។ Mask secrets, tokens, personal data និង IPs ប្រសិនបើចែករំលែក log សម្រាប់ជំនួយ។

## ៦. Updates និង Vulnerability Response

ប្រើ package manager របស់ distro ដើម្បីទទួល security updates។ មុន major upgrades សូម៖

1. ពិនិត្យ advisory/changelog របស់ vendor។
2. Backup និងសាកក្នុង staging/VM។
3. កំណត់ maintenance window និង downtime plan។
4. អនុវត្ត update តាម change process។
5. ផ្ទៀងផ្ទាត់ services និង logs ក្រោយ update។

កុំបន្ថែម random repositories ឬ scripts ពី Internet ដើម្បីឆ្លើយតបនឹង vulnerability ដោយមិនបញ្ជាក់ប្រភព។

## ៧. កិច្ចការអនុវត្ត

រត់ read-only checks៖

~~~bash
whoami
id
ls -ld "$HOME"
uptime
free -h
df -h
ss -tuln
~~~

បើប្រព័ន្ធប្រើ systemd សាកមើល running services និង warning logs។ សរសេរ short report ដែលមាន observation, time និង follow-up question។ លាក់ sensitive details មុនចែករំលែក។

## សង្ខេប

សុវត្ថិភាពមូលដ្ឋានរួមមាន least privilege, trusted updates, permissions, backups និងការគ្រប់គ្រង logs។ Monitoring ពិនិត្យ resources, services និង ports ជាមួយ context។ កុំបិទ controls ឬលុប logs ដើម្បីធ្វើឱ្យ warning បាត់។

## ឯកសារយោង

- [Ubuntu Security documentation](https://ubuntu.com/security)
- [Red Hat security documentation](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/)
- [CIS Benchmarks](https://www.cisecurity.org/cis-benchmarks)
