# មេរៀនទី ២៖ Terminal និង Command Line

## គោលបំណងមេរៀន

បន្ទាប់ពីរៀនចប់ អ្នកអាច៖

- យល់ពីទំនាក់ទំនងរវាង Terminal, Shell និង Command។
- អានផ្នែក Command, Option និង Argument។
- ប្រើ Command line ជាមួយ quotes, Tab completion និង command history។
- ពិនិត្យ command exit status និងស្វែងរកជំនួយ។
- ប្រើ Command មូលដ្ឋានដោយមិនធ្វើការផ្លាស់ប្ដូរប្រព័ន្ធដែលមិនចាំបាច់។

## ១. Terminal, Shell និង Command

Terminal ជាកម្មវិធីសម្រាប់បង្ហាញ prompt និងទទួលអត្ថបទពីអ្នកប្រើ។ Shell ដូចជា Bash ឬ Zsh អាន command ដែលអ្នកវាយ បកស្រាយ ហើយស្នើឱ្យប្រព័ន្ធដំណើរការ។ Command គឺជាកម្មវិធី ឬ built-in shell instruction ដែលធ្វើការងារ។

បន្ទាត់ prompt ឧទាហរណ៍៖

~~~text
user@computer:~$
~~~

សញ្ញា និងរូបរាង prompt អាចខុសគ្នាតាម Distribution និង shell។ សញ្ញា $ ជាញឹកញាប់បង្ហាញថាកំពុងប្រើ user ធម្មតា។ កុំចាត់ទុក prompt នេះជាអត្ថបទដែលត្រូវវាយ។

## ២. រចនាសម្ព័ន្ធ Command

Command ជាច្រើនមានទម្រង់៖

~~~text
command [options] [arguments]
~~~

ឧទាហរណ៍៖

~~~bash
ls -l /etc
~~~

- ls ជា command។
- -l ជា option ដែលស្នើឱ្យបង្ហាញព័ត៌មានលម្អិត។
- /etc ជា argument ឬទីតាំងដែល command ត្រូវធ្វើការ។

Option ខ្លីជាច្រើនអាចសរសេររួមគ្នាបាន ប្រសិនបើ command គាំទ្រ។ អាន manual មុនសន្មតថា options មានន័យដូចគ្នារវាង commands ផ្សេងៗ។

## ៣. ស្គាល់ Shell បច្ចុប្បន្ន និង Command

~~~bash
echo "$SHELL"
ps -p "$$" -o comm=
type cd
command -v ls
~~~

- echo "$SHELL" បង្ហាញ shell ដែលបានកំណត់ជាលំនាំដើមនៅ environment។
- ps បង្ហាញ process របស់ shell ដែលកំពុងដំណើរការ។
- type cd ជួយឱ្យដឹងថា cd ជា shell built-in។
- command -v ls បង្ហាញទីតាំង ឬប្រភេទ command ដែល shell នឹងប្រើ។

តម្លៃ $SHELL មិនចាំបាច់ជាភស្តុតាងនៃ shell process បច្ចុប្បន្នទាំងស្រុងទេ; ប្រើការពិនិត្យ process ប្រសិនបើត្រូវការដឹងឱ្យច្បាស់។

## ៤. Quotes និង Spaces

Shell បកស្រាយ spaces ជាការបំបែកពាក្យ។ ប្រសិនបើ filename ឬ argument មាន space សូមប្រើ quotes៖

~~~bash
printf '%s
' "My project folder"
~~~

- Single quotes រក្សាអក្សរខាងក្នុងជាអត្ថបទសាមញ្ញ។
- Double quotes អនុញ្ញាតឱ្យ shell ពង្រីក variables ដូចជា "$HOME"។
- Backslash អាចការពារតួអក្សរពិសេសមួយ ប៉ុន្តែ quotes ជាញឹកញាប់អានងាយជាង។

ឧទាហរណ៍៖

~~~bash
printf '%s
' '$HOME'
printf '%s
' "$HOME"
~~~

បន្ទាត់ទីមួយបង្ហាញអក្សរ $HOME តាមតួអក្សរ។ បន្ទាត់ទីពីរបង្ហាញតម្លៃ home directory។ ប្រើ quotes ជុំវិញ paths និង variables ដើម្បីជៀសវាងបញ្ហា spaces និង glob characters។

## ៥. Tab Completion និង History

- ចុច Tab ដើម្បីបំពេញ command ឬ filename ប្រសិនបើមានតែមួយជម្រើស។
- ចុច Tab ពីរដងក្នុង shell ខ្លះ ដើម្បីមើលជម្រើសដែលអាចបំពេញបាន។
- ប្រើ Up/Down ដើម្បីមើល command មុនៗ។
- ប្រើ history ដើម្បីមើលបញ្ជី command ដែល shell បានរក្សាទុក។
- ប្រើ Ctrl+C ដើម្បីបញ្ឈប់ command ដែលកំពុងរត់ក្នុង terminal ជាទូទៅ។
- ប្រើ Ctrl+L ដើម្បីសម្អាតការបង្ហាញលើអេក្រង់; វាមិនលុបឯកសារទេ។

កុំចែករំលែក screenshot ឬ history ដែលអាចមាន tokens, passwords, private paths ឬព័ត៌មានសម្ងាត់។

## ៦. Exit Status

Command ជាទូទៅបញ្ចប់ដោយផ្ដល់លេខ exit status។ លេខ 0 ជាញឹកញាប់មានន័យថាជោគជ័យ; លេខមិនសូន្យបង្ហាញថាមានលក្ខខណ្ឌមួយដែលត្រូវពិនិត្យ។

~~~bash
true
echo "$?"
false
echo "$?"
~~~

$? មានតម្លៃ exit status របស់ command មុនភ្លាមៗ។ បើរត់ command ផ្សេងមុនពិនិត្យ នោះតម្លៃនឹងត្រូវបានប្ដូរ។

## ៧. ជំនួយពី Shell និង Manual

ប្រើ help សម្រាប់ shell built-ins និង man សម្រាប់ commands ដែលមាន manual៖

~~~bash
help cd
man ls
ls --help
~~~

ចុច q ដើម្បីចេញពី man pager។ មិនមែន command ទាំងអស់មាន option --help ដូចគ្នាទេ។ នៅ Ubuntu/Debian អាចដំឡើង manual pages បន្ថែមតាម package manager ប្រសិនបើវាមិនមាន។

## ៨. ការប្រុងប្រយ័ត្នពេល copy command

មុន paste command ពី Website ឬមិត្តភក្តិ៖

1. អាន command ពេញលេញ និង arguments ទាំងអស់។
2. ស្វែងយល់ថាវាអាន បង្កើត កែ ឬលុបទិន្នន័យ។
3. ប្រយ័ត្ន command ដែលប្រើ sudo, redirection, pipe ទៅ shell ឬ recursive flags។
4. កុំរត់ script ដែលមិនទាន់ពិនិត្យ។
5. សាកល្បងក្នុង VM ឬ directory សាកល្បងមុន បើអាច។

Command line អនុញ្ញាតឱ្យធ្វើការងារមានប្រសិទ្ធភាព ប៉ុន្តែ command មួយខុសអាចប៉ះពាល់ឯកសារច្រើនបាន។

## ៩. កិច្ចការអនុវត្ត

រត់ commands ទាំងនេះ ហើយសរសេរអត្ថន័យរបស់លទ្ធផល៖

~~~bash
printf '%s
' "Hello from the terminal"
echo "$HOME"
pwd
type cd
command -v ls
true
echo "$?"
false
echo "$?"
man pwd
~~~

ចេញពី man ដោយចុច q។ សាក Tab completion នៅក្នុង home directory ដោយបំពេញឈ្មោះ directory ដែលមានស្រាប់។ កុំប្រើ command លុបឯកសារក្នុងលំហាត់នេះ។

## ១០. សង្ខេប

Terminal ជាផ្ទាំងសម្រាប់ប្រើ shell។ Command មានឈ្មោះ, options និង arguments។ Quotes ជួយឱ្យ spaces និង shell expansion ដំណើរការត្រឹមត្រូវ។ Tab completion និង history ជួយសន្សំពេល។ Exit status និង manual ជួយពិនិត្យលទ្ធផល និងស្វែងយល់ command មុនប្រើ។

## ឯកសារយោង

- [GNU Bash Reference Manual](https://www.gnu.org/software/bash/manual/bash.html)
- [GNU Coreutils Manual](https://www.gnu.org/software/coreutils/manual/coreutils.html)
