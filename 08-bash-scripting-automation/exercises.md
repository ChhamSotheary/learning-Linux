# លំហាត់មេរៀនទី ៨៖ Bash Scripting និង Automation

## ផ្នែក A៖ សំណួរ
1. Shebang មានតួនាទីអ្វី?
2. តើ $0, $1 និង $# មានន័យដូចម្តេច?
3. ហេតុអ្វីគួរ quote "$variable"?
4. តើ exit status 0 ជាទូទៅមានន័យដូចម្តេច?
5. ហេតុអ្វី cron script គួរកំណត់ paths និង environment ឱ្យច្បាស់?

## ផ្នែក B៖ បង្កើត Script

បង្កើត directory សាកល្បង ហើយសរសេរ report.sh ដែលត្រូវការ argument មួយជាថត output។ បើ argument ខ្វះ បង្ហាញ usage ទៅ stderr និងចេញ status មិនសូន្យ។ បើមាន argument បង្កើតថតក្នុង workspace ហើយសរសេរ hostname/date ទៅ report.txt។

សាកល្បង៖

~~~bash
bash report.sh
bash report.sh "$HOME/linux-practice/lesson-08/output"
printf 'status=%s\n' "$?"
cat "$HOME/linux-practice/lesson-08/output/report.txt"
~~~

អាន script ទាំងមូលមុនដំណើរការ ហើយធានាថា output ស្ថិតក្នុង workspace ផ្ទាល់ខ្លួន។

## ផ្នែក C៖ Code Review

- តើ variables ត្រូវបាន quote ទេ?
- តើ errors បង្ហាញទៅ stderr ទេ?
- តើ arguments ត្រូវបាន validate ទេ?
- តើ paths អាចសរសេរទៅក្រៅ workspace ដោយចៃដន្យទេ?
- តើមាន secrets hard-coded ទេ?

## លក្ខខណ្ឌបញ្ចប់

- Script អាចរត់បានតាម Bash និង execute permission។
- ករណី argument ខ្វះត្រូវបានដោះស្រាយច្បាស់។
- Output ត្រូវបានបង្កើតតែក្នុង directory ដែលបានកំណត់។
- អាចពន្យល់ exit status និង quoting។
