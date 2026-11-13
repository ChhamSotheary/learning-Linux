# លំហាត់មេរៀនទី ៤៖ Users, Groups និង Permissions

អនុវត្តក្នុង directory ផ្ទាល់ខ្លួនប៉ុណ្ណោះ។ កុំប្រើ sudo ឬកែ system files ក្នុងលំហាត់នេះ។

## ផ្នែក A៖ សំណួរ

1. UID និង GID ជាអ្វី?
2. តើ ls -l បង្ហាញ permission របស់ក្រុមណាខ្លះ?
3. សិទ្ធិ x លើ directory អនុញ្ញាតអ្វី?
4. តើ chmod 640 មានន័យដូចម្តេច?
5. ហេតុអ្វី 777 ជាទូទៅមិនមែនជា default ល្អ?
6. តើ umask ប៉ះពាល់អ្វី?

## ផ្នែក B៖ អនុវត្ត

~~~bash
mkdir -p "$HOME/linux-practice/exercise-04"
cd "$HOME/linux-practice/exercise-04"
printf '%s
' "Private practice note" > note.txt
id
groups
ls -l note.txt
chmod 600 note.txt
ls -l note.txt
chmod g+r note.txt
ls -l note.txt
umask
~~~

កត់ត្រា permission មុន និងក្រោយ chmod នីមួយៗ។ ពន្យល់ថា owner, group និង others អាចធ្វើអ្វីបាន។

## លក្ខខណ្ឌបញ្ចប់

- អាចអាន owner/group/others permission ក្នុង ls -l។
- អាចពន្យល់ r/w/x លើ files និង directories។
- អាចប្រើ chmod numeric និង symbolic លើ file ផ្ទាល់ខ្លួន។
- មិនប្រើ privileged command ដោយគ្មានមូលហេតុ។
