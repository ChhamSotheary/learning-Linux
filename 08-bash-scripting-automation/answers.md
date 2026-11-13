# ចម្លើយណែនាំ៖ មេរៀនទី ៨

## ផ្នែក A

1. Shebang បញ្ជាក់ interpreter ដែលប្រព័ន្ធគួរប្រើដើម្បីរត់ script។
2. $0 ជាឈ្មោះ script, $1 ជា argument ទីមួយ, $# ជាចំនួន arguments។
3. Quotes រក្សា whitespace និងទប់ shell word splitting/globbing លើ variable value។
4. Exit status 0 ជាទូទៅបង្ហាញជោគជ័យ; non-zero ជាទូទៅបង្ហាញ error ឬលទ្ធផលផ្សេង។
5. Cron environment តិចជាង interactive shell ហើយអាចមាន PATH/working directory ខុស។ កំណត់ឱ្យច្បាស់ជួយឱ្យ run ទៀងទាត់ និង debug ងាយ។

## ផ្នែក B

គំរូចម្លើយ៖

~~~bash
#!/usr/bin/env bash
set -u

if [ "$#" -ne 1 ]; then
    printf 'Usage: %s OUTPUT_DIR\n' "$0" >&2
    exit 2
fi

output_dir=$1
mkdir -p -- "$output_dir" || exit 1
{
    hostname
    date
} > "$output_dir/report.txt" || exit 1

printf 'Report written to %s\n' "$output_dir"
~~~

ពិនិត្យ path របស់ output_dir មុនរត់។ Project ពិតអាចត្រូវការ validation/allowlist បើ user មិនគួរកំណត់ output path ដោយសេរី។
