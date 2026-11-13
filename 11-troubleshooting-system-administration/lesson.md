# មេរៀនទី ១១៖ Troubleshooting និង System Administration

## គោលបំណង

- ប្រើ troubleshooting workflow ដែលមានលំដាប់។
- ប្រមូល facts ពី services, logs, resources, storage និង network។
- កំណត់បញ្ហា និងសរសេរ incident notes។
- រៀបចំការផ្លាស់ប្ដូរប្រព័ន្ធដោយមាន backup, approval និង rollback plan។
- ជៀសវាងការសន្និដ្ឋាន ឬធ្វើ action ដោយគ្មានភស្តុតាង។

## ១. Troubleshooting Workflow

1. កំណត់អ្វីដែលបរាជ័យ និងអ្នកណារងផលប៉ះពាល់។
2. កត់ពេលវេលា និងអ្វីដែលបានផ្លាស់ប្ដូរថ្មីៗ។
3. ប្រមូលព័ត៌មាន read-only មុន។
4. ប្រៀបធៀបជាមួយ baseline និងស្ថានភាពធម្មតា។
5. បង្កើត hypothesis មួយដែលអាចសាកល្បងបាន។
6. ធ្វើ change តូចបំផុតដែលមានសិទ្ធិ និងគោលបំណងច្បាស់។
7. ផ្ទៀងផ្ទាត់លទ្ធផល និងចងក្រង recovery/rollback។
8. កត់អ្វីដែលបានរៀន ដើម្បីកុំឱ្យកើតឡើងម្ដងទៀត។

កុំចាប់ផ្ដើមដោយ restart, delete logs ឬបិទ firewall។ សកម្មភាពទាំងនេះអាចប៉ះពាល់អ្នកប្រើ និងលុបភស្តុតាង។

## ២. ពិនិត្យ System Health

~~~bash
uptime
free -h
df -h
ps -ef
ss -tuln
~~~

ប្រៀបធៀបជាមួយ workload។ ឧទាហរណ៍ disk usage ខ្ពស់អាចប៉ះ service សរសេរទិន្នន័យ; memory ទំនេរតិចតែម្ដងមិនប្រាកដថាប្រព័ន្ធខូចទេ ព្រោះ Linux ប្រើ memory សម្រាប់ cache ផងដែរ។

## ៣. ពិនិត្យ Service និង Logs

លើ systemd systems៖

~~~bash
systemctl --failed
systemctl status SERVICE_NAME
journalctl -u SERVICE_NAME -b -n 100
~~~

ជំនួស SERVICE_NAME ដោយ service ដែលអ្នកមានសិទ្ធិពិនិត្យ។ បើមិនប្រើ systemd សូមប្រើ tools របស់ init/service manager របស់ distribution។

រក្សាពេលវេលា និង error context ជុំវិញ incident។ កុំ paste full logs ដោយមិនពិនិត្យ secrets និង personal information។

## ៤. ពិនិត្យ Boot និង Hardware Messages

~~~bash
journalctl -b -p err
dmesg --level=err,warn
~~~

ការអាន kernel logs អាចត្រូវការសិទ្ធិ។ កុំប្រើ sudo ដោយស្វ័យប្រវត្តិ; ប្រសិនបើ permission មិនគ្រប់ សូមស្នើ administrator ពិនិត្យ។ ពិនិត្យថា error កើតឡើងជាបន្ត ឬមានតែម្តង។

## ៥. Network Troubleshooting

ប្រើ commands ពីមេរៀន Networking៖ ip addr, ip route, getent hosts, ss និង curl ទៅ endpoint ដែលអ្នកមានសិទ្ធិ។ បំបែកបញ្ហាជាផ្នែក៖ interface, route/gateway, DNS, firewall, remote service និង application configuration។

កុំបិទ firewall ឬស្កេនបណ្ដាញដើម្បីសាកល្បង។ ស្នើ network owner ឬ administrator ពិនិត្យ rule តាម change process។

## ៦. Change Management សម្រាប់ Admin

មុនប្ដូរ system config ឬ service៖

- បញ្ជាក់ owner និងសិទ្ធិ។
- ពិពណ៌នា expected impact និង downtime។
- Backup configuration និងទិន្នន័យពាក់ព័ន្ធ។
- សាកល្បងក្នុង VM/staging បើអាច។
- កំណត់ rollback step មុនអនុវត្ត។
- អនុវត្តក្នុង maintenance window។
- ផ្ទៀងផ្ទាត់ health និង logs ក្រោយ change។
- កត់ថាតើ change បានជោគជ័យ និងត្រូវការតាមដានអ្វី។

## ៧. Incident Notes Template

~~~text
Time/timezone:
System/service:
Observed symptom:
User/business impact:
Recent changes:
Commands/data collected:
Sensitive details removed:
Hypothesis:
Action taken (with approval):
Result:
Rollback/follow-up:
~~~

Facts និង hypothesis ត្រូវសម្គាល់ដាច់ពីគ្នា។ កុំរួមបញ្ចូល passwords, tokens, private keys ឬ full personal logs។

## ៨. កិច្ចការអនុវត្ត

ស្រមៃថា web service មួយមិនអាចឆ្លើយតប។ ក្នុង VM ឬលើម៉ាស៊ីនដែលអ្នកមានសិទ្ធិ សូមប្រមូល read-only evidence៖

1. uptime, free -h និង df -h។
2. systemctl status service បើមាន។
3. journalctl logs សម្រាប់ service និង boot បច្ចុប្បន្ន។
4. ss -tuln ដើម្បីមើល listening ports។
5. ពិនិត្យ DNS/route ប្រសិនបើបញ្ហាពាក់ព័ន្ធ network។
6. បំពេញ incident notes template ដោយលាក់ sensitive data។
7. កុំ restart ឬកែ config ក្នុងលំហាត់នេះ; រៀបរាប់ថាតើត្រូវការការអនុម័តអ្វីមុន change។

## សង្ខេប

System administration ត្រូវការភស្តុតាង ការគ្រប់គ្រងសិទ្ធិ និងការកត់ត្រា។ ពិនិត្យ health, service status, logs និង network មុន change។ Backup, approval, maintenance window និង rollback plan ជួយកាត់បន្ថយហានិភ័យ។

## ឯកសារយោង

- [systemctl manual](https://www.freedesktop.org/software/systemd/man/latest/systemctl.html)
- [journalctl manual](https://www.freedesktop.org/software/systemd/man/latest/journalctl.html)
- [Linux System Administrator's Guide](https://tldp.org/LDP/sag/html/)
