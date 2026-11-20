# Lab ១៣៖ គ្រប់គ្រង Software ជាមួយ DNF (Manage Software with DNF)

## គោលបំណង
ស្គាល់ package, repository និងប្រើ DNF ដើម្បីស្វែងរកព័ត៌មាន software នៅ RHEL។

## ១. ពិនិត្យ DNF និងប្រព័ន្ធ
```bash
dnf --version
cat /etc/redhat-release
```
RHEL ប្រើ RPM packages និង DNF សម្រាប់គ្រប់គ្រង software និង dependencies។

## ២. ស្វែងរក package
```bash
dnf search nano
dnf info nano
```
លទ្ធផលអាស្រ័យលើ repository ដែលបានកំណត់ និង subscription/access របស់ប្រព័ន្ធ។

## ៣. រាយ package ដែលបានដំឡើង
```bash
dnf list installed
rpm -qa | head
```
`rpm -qa` រាយ package ដែលបានដំឡើងតាម RPM database។

## ៤. ពិនិត្យ repository
```bash
dnf repolist
```
បើ repository មិនមាន ឬមិនអាចចូលបាន សូមពិនិត្យការចុះឈ្មោះ Red Hat Subscription និង network។ កុំប្រើ repository មិនទុកចិត្ត។

## ៥. ដំឡើង package (ជាជម្រើសក្នុង VM)
មុនដំឡើង សូមពិនិត្យព័ត៌មាន package និងទំហំទំនេរ។ ត្រូវការ sudo និង repository ដែលអាចប្រើបាន។
```bash
sudo dnf install nano
```
ពិនិត្យ transaction summary មុនបញ្ជាក់។ អាចចុច `n` ដើម្បីបោះបង់។

## ៦. ធ្វើបច្ចុប្បន្នភាព
```bash
dnf check-update
```
Exit status អាចបង្ហាញថាមាន updates ដោយមិនមានន័យថា command បរាជ័យ។ កុំធ្វើ full system upgrade លើប្រព័ន្ធសំខាន់ដោយគ្មាន backup និង maintenance plan។

## លំហាត់
1. ពិនិត្យ version របស់ DNF។
2. ស្វែងរក package `nano`។
3. ពិនិត្យព័ត៌មាន package។
4. រាយ repository ដែលអាចប្រើបាន។
5. ពន្យល់ភាពខុសគ្នារវាង package និង repository។

## ពិនិត្យចំណេះដឹង
- [ ] ខ្ញុំអាចប្រើ `dnf search` និង `dnf info`។
- [ ] ខ្ញុំអាចពិនិត្យ installed packages។
- [ ] ខ្ញុំយល់ពី repository និង dependencies។

**សុវត្ថិភាព:** ដំឡើង software តែពី repository ដែលទុកចិត្ត។ ពិនិត្យ transaction មុនបញ្ជាក់។
