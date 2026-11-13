# ម៉ូឌុលទី ១៨៖ Linux ក្រោយឆាក — ចំណុចដែលវគ្គទូទៅរំលង

នេះជាម៉ូឌុលអនុវត្តសម្រាប់យល់ពីអ្វីដែលកើតក្នុង Linux ពេលកម្មវិធីដំណើរការ។ មិនមានអ្វី “សម្ងាត់” ទេ; ប្រធានបទទាំងនេះត្រូវការពេល និង lab ច្រើន ដូច្នេះវគ្គមូលដ្ឋានជាច្រើនមិនបានចូលជ្រៅ។

## មេរៀន

1. [ពេលរត់កម្មវិធី៖ ELF និង Dynamic Linker](lesson-01-running-a-program.md)
2. [Virtual Memory និង Memory Map](lesson-02-virtual-memory.md)
3. [Scheduler និង Context Switch](lesson-03-scheduler.md)
4. [File Descriptor និង VFS](lesson-04-file-descriptors-vfs.md)
5. [ពី write() ទៅ Disk៖ Page Cache និង I/O](lesson-05-write-to-disk.md)
6. [ពី Socket ទៅ Network Interface](lesson-06-socket-to-network.md)
7. [Tracing៖ strace, perf និង eBPF](lesson-07-tracing.md)
8. [Security Boundary និង Threat Model របស់ Kernel](lesson-08-kernel-security-boundary.md)
9. [Lab សរុប៖ ស៊ើបអង្កេតកម្មវិធីមួយ](capstone-lab.md)

## របៀបប្រើ

អានមេរៀនតាមលំដាប់ ហើយរត់ command តែលើ process, file និង VM របស់អ្នក។ command ត្រូវបានជ្រើសជាការអាន/សង្កេតជាចម្បង។ កុំប្រើ privileged tracing, kernel module, exploit ឬប្ដូរ security policy លើប្រព័ន្ធផលិតកម្ម។

## គោលដៅ

ចប់ម៉ូឌុលនេះ អ្នកអាចពន្យល់ពីដំណើរការកម្មវិធីពី ELF loader ទៅ syscalls, អាន memory map, យល់ពី file descriptor និង I/O buffering, និងប្រមូល evidence ដោយបែងចែកការវាស់ចេញពីសម្មតិកម្ម។

## ឯកសារយោងផ្លូវការ

- [ELF specification overview in Linux man-pages](https://man7.org/linux/man-pages/man5/elf.5.html)
- [proc_pid_maps(5)](https://man7.org/linux/man-pages/man5/proc_pid_maps.5.html)
- [Linux scheduler documentation](https://docs.kernel.org/scheduler/)
- [VFS documentation](https://docs.kernel.org/filesystems/vfs.html)
- [BPF documentation](https://docs.kernel.org/bpf/)
- [Capabilities(7)](https://man7.org/linux/man-pages/man7/capabilities.7.html)
- [Seccomp(2)](https://man7.org/linux/man-pages/man2/seccomp.2.html)
