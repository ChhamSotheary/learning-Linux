# មេរៀនទី ១៖ Incident Response និង Evidence Timeline

Incident response ចាប់ផ្តើមពីការកំណត់ impact, scope និងពេលវេលា មុនប្ដូរប្រព័ន្ធ។ គោលបំណងគឺស្ដារសេវាដោយមានការគ្រប់គ្រង ខណៈរក្សាភស្តុតាងដែលចាំបាច់។ អនុវត្តតាមនីតិវិធីរបស់អង្គភាព និងរក្សា chain of custody សម្រាប់ករណីស៊ើបអង្កេតផ្លូវការ។

## Snapshot អានប៉ុណ្ណោះ

~~~bash
date -Is
uptime
systemctl --failed
journalctl -b -p err --no-pager
df -h
free -h
ss -s
~~~

កត់ម៉ោង, command, អ្នករត់, output និង timezone។ កុំបង្ហោះ secret, token, public IP ឬព័ត៌មានអ្នកប្រើ។ កុំ kill process, reboot ឬលុប log មុនកត់ impact និងទទួលការអនុម័តតាមការងារ។

## លំហាត់

ស្រមៃថា web service មិនឆ្លើយ។ បង្កើត timeline ដោយចាប់ពី report, checks, evidence, mitigation ដែលអាចធ្វើបាន និងលក្ខខណ្ឌ rollback។ បែងចែក observation ពី hypothesis។
