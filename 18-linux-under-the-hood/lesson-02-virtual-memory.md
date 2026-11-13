# មេរៀនទី ២៖ Virtual Memory និង Memory Map

Process នីមួយៗមាន virtual address space ផ្ទាល់ខ្លួន។ Page table ភ្ជាប់ virtual pages ទៅ physical memory ឬ mapping ផ្សេងៗ។ ដូច្នេះ address ដូចគ្នាក្នុង process ពីរមិនចាំបាច់សំដៅទៅ physical memory ដូចគ្នាទេ។ Memory map រួមមាន executable, shared library, heap, stack, mmap files និង kernel-managed regions ដែលមើលឃើញខ្លះៗ។

## មើល process ផ្ទាល់ខ្លួន

~~~bash
cat /proc/self/maps | head -n 20
cat /proc/self/smaps_rollup
~~~

/proc/self/maps បង្ហាញ range, permission, offset និង path ប្រសិនបើ mapping ភ្ជាប់ file។ អក្សរ r/w/x និង p/s ជួយបកស្រាយ permission និង private/shared mapping។ Mapping ដែលមិនបង្ហាញ path អាចជា anonymous mapping មិនមែនមានន័យថា “គ្មានអ្វីនៅទីនោះ” ទេ។

ចាប់ផ្តើម process ដែលនៅរង់ចាំក្នុង shell ផ្ទាល់ខ្លួន ហើយ inspect PID៖

~~~bash
sleep 60 &
pid=$!
cat /proc/$pid/maps | head
kill "$pid"
~~~

នេះបង្កើត និងបិទ process test របស់អ្នកប៉ុណ្ណោះ។ កុំអាន memory របស់ process អ្នកដទៃដោយគ្មានសិទ្ធិ។

## លំហាត់

1. រក mapping របស់ executable, shared libraries និង stack។
2. ប្រៀបធៀប permission នៃ mapping ទាំងនោះ។
3. ពន្យល់ថាហេតុអ្វី virtual memory ធ្វើឱ្យ process isolation កាន់តែងាយ ប៉ុន្តែមិនធានា security ដោយខ្លួនឯង។
