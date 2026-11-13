# មេរៀនទី ៨៖ Bash Scripting និង Automation

## គោលបំណង
- បង្កើត Bash script សាមញ្ញ។
- ប្រើ variables, arguments, conditionals និង loops។
- ប្រើ quotes ដើម្បីការពារ paths ដែលមាន spaces។
- កំណត់ exit status និងសាកល្បងក្នុង workspace។
- យល់ពីការប្រុងប្រយ័ត្នមុនកំណត់ automation schedule។

## ១. បង្កើត Script ដំបូង

~~~bash
#!/usr/bin/env bash
printf '%s\n' "Hello from Bash"
~~~

Shebang ជាបន្ទាត់ដំបូងដែលប្រាប់ប្រព័ន្ធឱ្យប្រើ interpreter។ រត់ដោយ bash hello.sh ឬផ្ដល់ execute permission ដោយ chmod u+x hello.sh រួចរត់ ./hello.sh។ កុំដំណើរការ script ដែលមិនទាន់អាន ឬមិនទុកចិត្ត។

## ២. Variables និង Quotes

~~~bash
name="Linux learner"
printf 'Hello, %s\n' "$name"
~~~

កុំដាក់ spaces ជុំវិញសញ្ញា = ពេលកំណត់ variable ក្នុង Bash។ ប្រើ "$name" ជាទម្លាប់ ដើម្បីរក្សាតម្លៃជាពាក្យតែមួយ និងការពារ word splitting/globbing។

## ៣. Command-line Arguments

~~~bash
#!/usr/bin/env bash
set -u

if [ "$#" -lt 1 ]; then
    printf 'Usage: %s NAME\n' "$0" >&2
    exit 2
fi

printf 'Hello, %s\n' "$1"
~~~

- $0 ជាឈ្មោះ script។
- $1 ជា argument ទីមួយ។
- $# ជាចំនួន arguments។
- exit 0 ជោគជ័យជាទូទៅ; លេខផ្សេងបង្ហាញលទ្ធផល/កំហុសផ្សេង។

Validate input មុនប្រើជាផ្លូវ file ឬបញ្ជូនទៅ command ផ្សេង។

## ៤. Conditionals និង Loops

~~~bash
if [ -f "$1" ]; then
    printf 'File exists: %s\n' "$1"
else
    printf 'No regular file at: %s\n' "$1"
fi

for item in alpha beta gamma; do
    printf '%s\n' "$item"
done
~~~

អាន Bash manual សម្រាប់ test operators និង error handling; syntax របស់ test brackets និង double brackets មិនដូចគ្នាទាំងស្រុងទេ។

## ៥. គ្រប់គ្រងកំហុស និងសុវត្ថិភាព

~~~bash
set -euo pipefail
~~~

ជាទូទៅ options ទាំងនេះបញ្ឈប់ script ពេល command error, variable មិនកំណត់ ឬ pipeline មានបញ្ហា។ ប៉ុន្តែ exit-on-error មានករណី behavior ពិសេស; វាមិនជំនួសការគ្រប់គ្រង error ដោយច្បាស់ទេ។

- ប្រើ absolute paths ឬកំណត់ working directory ឱ្យច្បាស់។
- quote variables ដូចជា "$output_dir"។
- Validate arguments និងបង្ហាញ usage message។
- កុំសរសេរ/លុបទិន្នន័យក្រៅ workspace ដែលមានបំណង។
- កុំ hard-code secrets ក្នុង script។
- កត់ error ទៅ stderr ដោយប្រើ file descriptor 2។

## ៦. Automation

Automation អាចដំណើរការតាម cron ឬ systemd timers។ មុន schedule សូមបញ្ជាក់ script path, user, environment និង working directory។ កំណត់ logs និង failure notification ហើយសាកល្បងដោយដៃមុន។ Cron environment ជាទូទៅមាន PATH តិចជាង interactive shell; ប្រើ full paths និងកំណត់ environment ច្បាស់។

កុំ schedule command ដែលបំផ្លាញទិន្នន័យដោយគ្មាន backup និង recovery plan។

## ៧. កិច្ចការអនុវត្ត

ក្នុង $HOME/linux-practice/lesson-08 បង្កើត report.sh ដែលទទួល output directory ជា argument។ បើ argument ខ្វះ បង្ហាញ usage ហើយចេញដោយ status មិនសូន្យ។ បើមាន argument បង្កើត directory ក្នុង workspace របស់អ្នក សរសេរ hostname និង date ទៅ report.txt ហើយចេញដោយ status 0។

មុនអនុញ្ញាតឱ្យ script រត់ សូមអានគ្រប់បន្ទាត់ និងពិនិត្យ path។

## សង្ខេប

Bash script ជា file មាន commands ដែលអាចរត់តាមលំដាប់។ Variables និង arguments ធ្វើឱ្យ script បត់បែនបាន។ Quotes ការពារ paths និង values។ Validate input, គ្រប់គ្រង exit codes និងសាកល្បងក្នុង workspace មុន schedule automation។

## ឯកសារយោង

- [GNU Bash Reference Manual](https://www.gnu.org/software/bash/manual/bash.html)
- [ShellCheck](https://www.shellcheck.net/)
- [Cron manual](https://man7.org/linux/man-pages/man8/cron.8.html)
