# លំហាត់មេរៀនទី ៦៖ Processes, Services និង Logs

## ផ្នែក A៖ សំណួរ

1. PID ជាអ្វី?
2. តើ ps, top និង pgrep ជួយអ្វីខ្លះ?
3. តើ SIGTERM ខុសពី SIGKILL ដូចម្តេច?
4. តើ systemctl status និង systemctl restart ខុសគ្នាយ៉ាងណា?
5. ហេតុអ្វីត្រូវពិនិត្យ logs មុនចាប់ផ្ដើម service ឡើងវិញ?

## ផ្នែក B៖ អនុវត្តដោយសុវត្ថិភាព

~~~bash
ps -ef
sleep 60 &
jobs
ps -p "$!" -o pid,stat,comm
kill -TERM "$!"
~~~

បន្ទាប់ពី kill សូមពិនិត្យ jobs ឬ ps ម្ដងទៀត។ បើ process បានបញ្ចប់រួចហើយ សូមកត់ត្រាថាវាបញ្ចប់មុនពេល kill។

## ផ្នែក C៖ ពិនិត្យដោយមិនប្ដូរស្ថានភាព

បើម៉ាស៊ីនប្រើ systemd៖

~~~bash
systemctl status
systemctl list-units --type=service --state=running
journalctl -b -n 20
~~~

កុំប្រើ stop/restart/disable ក្នុងលំហាត់។ កត់ service មួយដែលកំពុងរត់ និង message មួយដែលមិនមានព័ត៌មានរសើប។

## លក្ខខណ្ឌបញ្ចប់

- អាចពិនិត្យ processes និង background jobs។
- អាចបញ្ឈប់ process សាកល្បងដែលខ្លួនបង្កើត។
- អាចពិនិត្យ service/log status ដោយមិនប្ដូរស្ថានភាពប្រព័ន្ធ។
- អាចពន្យល់ពីការការពារ sensitive information ក្នុង logs។
