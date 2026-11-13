# មេរៀនទី ២៖ Filesystem, Inode និង Journal

Directory ភ្ជាប់ឈ្មោះទៅ inode; inode កាន់ metadata និង pointers ទៅ data blocks (របៀបពិតអាស្រ័យលើ filesystem)។ Permission, owner, timestamps, hard links និង symlink ជាផ្នែកនៃ metadata/namespace។ Journal filesystem ប្រើ log mechanism ដើម្បីជួយស្ដារភាពស្ថិរភាព metadata ក្រោយ crash ប៉ុន្តែមិនស្មើនឹង backup ទេ។

~~~bash
stat /etc/hosts
findmnt -no SOURCE,FSTYPE,OPTIONS /
df -i /
~~~

Hard link ចែក inode ដូចគ្នា; symlink ជា file ដែលមាន path ទៅគោលដៅ។ ការលុបឈ្មោះមួយមិនចាំបាច់លុបទិន្នន័យរហូតទាល់តែ reference បាត់ទាំងអស់ និង file descriptor បិទ។

## លំហាត់

បង្កើត file សាកល្បងក្នុង directory របស់អ្នក ហើយប្រៀបធៀប stat របស់ file, hard link និង symlink។ លុបតែឯកសារសាកល្បងរបស់អ្នកក្រោយពិនិត្យ path។
