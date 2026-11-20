# Lab ៧៖ តាមដាន និងគ្រប់គ្រង Processes (Monitor and Manage Processes)

## គោលបំណង
ស្គាល់ process, PID, parent process, foreground/background និងការបញ្ឈប់ process ដោយសុវត្ថិភាព។

## ១. មើល Processes
```bash
ps
ps -ef
ps -u "$USER"
top
```
`ps` បង្ហាញ snapshot នៃ processes។ `top` បង្ហាញការប្រើ CPU និង memory ជាបន្តបន្ទាប់; ចុច `q` ដើម្បីចេញ។

## ២. ស្វែងរក Process
```bash
pgrep -a bash
ps -p "$$" -o pid,ppid,comm
```
PID ជាលេខសម្គាល់ process។ PPID ជា PID របស់ parent process។

## ៣. បង្កើត Process សាកល្បង
```bash
sleep 300 &
jobs
pgrep -a sleep
```
សញ្ញា `&` ដំណើរការ command នៅ background។ កត់ PID ដែលបានបង្ហាញ។

## ៤. បញ្ឈប់ Process សាកល្បង
```bash
pkill -TERM -x sleep
pgrep -a sleep
```
ប្រើតែពេលគ្មាន process sleep ផ្សេងដែលអ្នកចង់រក្សាទុក។ ជម្រើសប្រុងប្រយ័ត្នជាងនេះគឺប្រើ `kill -TERM PID` ដោយបញ្ចូល PID របស់ process ដែលអ្នកបានបង្កើតផ្ទាល់។ TERM ស្នើឱ្យ process បញ្ចប់ដោយស្អាត។

## ៥. លំហាត់
1. ប្រើ `ps -ef` ហើយរក PID របស់ process មួយ។
2. បើក `top` និងកំណត់ថា process ណាប្រើ CPU ខ្ពស់។
3. បង្កើត `sleep 120 &` ហើយស្វែងរក PID។
4. បញ្ឈប់តែ PID នោះដោយ `kill -TERM PID`។
5. ពន្យល់ភាពខុសគ្នារវាង PID និង PPID។

## ពិនិត្យចំណេះដឹង
- [ ] ខ្ញុំអាចប្រើ ps និង top។
- [ ] ខ្ញុំយល់ពី foreground/background។
- [ ] ខ្ញុំអាចបញ្ឈប់ process សាកល្បងដោយកំណត់ PID ត្រឹមត្រូវ។

**សុវត្ថិភាព:** កុំសាក `kill -9` ឬសម្លាប់ process ប្រព័ន្ធដោយមិនយល់ពីផលប៉ះពាល់។
