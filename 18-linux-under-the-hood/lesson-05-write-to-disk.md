# មេរៀនទី ៥៖ ពី write() ទៅ Disk — Page Cache និង I/O

ពេលកម្មវិធីហៅ write() ទិន្នន័យអាចត្រូវបាន copy ទៅ page cache ហើយ kernel សរសេរទៅ storage ពេលក្រោយ។ លទ្ធផលជោគជ័យពី write មិនតែងមានន័យថាទិន្នន័យបានចុះទៅ physical media ភ្លាមៗទេ។ fsync/fdatasync ជួយស្នើឱ្យ kernel synchronize file data/metadata តាម semantics របស់ filesystem និង device; durability ក៏អាស្រ័យលើ hardware/cache និង error handling ផងដែរ។

## សង្កេតពីប្រព័ន្ធ

~~~bash
grep -E 'Dirty|Writeback|Cached' /proc/meminfo
iostat -xz 1 3
vmstat 1 5
~~~

iostat មកពី sysstat ហើយអាចមិនមាន។ កុំ install ឬប្ដូរ I/O scheduler ក្នុង lab នេះ។ Counter ជា snapshot/trend; ត្រូវប្រៀបធៀបតាមពេល និង workload។

## លំហាត់

1. ពន្យល់ភាពខុសគ្នារវាង “write បានជោគជ័យ” និង “data durable”។
2. ប្រមូល Dirty/Writeback ក្នុងពេលធម្មតា ហើយកត់ observation។
3. តើហេតុអ្វីការបិទភ្លើង ឬ device failure អាចធ្វើឱ្យការសន្និដ្ឋានពី filesystem syscall មិនគ្រប់គ្រាន់?
