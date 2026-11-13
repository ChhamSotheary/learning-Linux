# ចម្លើយណែនាំ៖ មេរៀនទី ៤

## ផ្នែក A

1. UID ជា user identifier; GID ជា group identifier ដែលប្រព័ន្ធប្រើសម្គាល់ accounts និង groups។
2. ls -l បង្ហាញ permissions សម្រាប់ owner, group និង others បន្ទាប់ពី file type indicator។
3. x លើ directory ជួយឱ្យចូលឆ្លង directory និង access entries តាម permissions ផ្សេងទៀត។
4. 640 មានន័យថា owner rw-, group r-- និង others ---។
5. 777 ផ្ដល់ read/write/execute ទៅគ្រប់ក្រុម ដែលអាចបង្កើតការកែប្រែ ឬការចូលប្រើមិនចាំបាច់។
6. umask ដក permissions ពី default mode ដែលប្រព័ន្ធប្រើពេលបង្កើត file ឬ directory ថ្មី។

## ផ្នែក B

- មុន chmod 600 លទ្ធផលអាស្រ័យលើ umask និង default mode។
- ក្រោយ chmod 600 file គួរមាន rw-------៖ owner អាន/សរសេរ, group និង others គ្មានសិទ្ធិ។
- ក្រោយ chmod g+r file គួរមាន rw-r-----៖ owner អាន/សរសេរ, group អាន និង others គ្មានសិទ្ធិ។

បើលទ្ធផលខុស សូមពិនិត្យថាអ្នកបានជ្រើស file ត្រឹមត្រូវ និង filesystem គាំទ្រ POSIX permissions ដែរឬទេ។ WSL/Windows mounts អាចមាន behavior ខុសពី Linux filesystem ធម្មតា។
