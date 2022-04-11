The common predefined macros are GNU C extensions. They are available with the same meanings regardless of the machine or operating system on which you are using GNU C or GNU Fortran. Their names all start with double underscores.



__COUNTER__

This macro expands to sequential integral values starting from 0. In conjunction with the ## operator, this provides a convenient means to generate unique identifiers. Care must be taken to ensure that __COUNTER__ is not expanded prior to inclusion of precompiled headers which use it. Otherwise, the precompiled headers will not be used.

__GFORTRAN__

The GNU Fortran compiler defines this.

__GNUC__

__GNUC_MINOR__

__GNUC_PATCHLEVEL__

These macros are defined by all GNU compilers that use the C preprocessor: C, C++, Objective-C and Fortran. Their values are the major version, minor version, and patch level of the compiler, as integer constants. For example, GCC 3.2.1 will define __GNUC__ to 3, __GNUC_MINOR__ to 2, and __GNUC_PATCHLEVEL__ to 1. These macros are also defined if you invoke the preprocessor directly.

__GNUC_PATCHLEVEL__ is new to GCC 3.0; it is also present in the widely-used development snapshots leading up to 3.0 (which identify themselves as GCC 2.96 or 2.97, depending on which snapshot you have).



If all you need to know is whether or not your program is being compiled by GCC, or a non-GCC compiler that claims to accept the GNU C dialects, you can simply test __GNUC__. If you need to write code which depends on a specific version, you must be more careful. Each time the minor version is increased, the patch level is reset to zero; each time the major version is increased (which happens rarely), the minor version and patch level are reset. If you wish to use the predefined macros directly in the conditional, you will need to write it like this:



          /* Test for GCC > 3.2.0 */

          #if __GNUC__ > 3 || \

              (__GNUC__ == 3 && (__GNUC_MINOR__ > 2 || \

                                 (__GNUC_MINOR__ == 2 && \

                                  __GNUC_PATCHLEVEL__ > 0))

Another approach is to use the predefined macros to calculate a single number, then compare that against a threshold:



          #define GCC_VERSION (__GNUC__ * 10000 \

                               + __GNUC_MINOR__ * 100 \

                               + __GNUC_PATCHLEVEL__)

          ...

          /* Test for GCC > 3.2.0 */

          #if GCC_VERSION > 30200

Many people find this form easier to understand.



__GNUG__

The GNU C++ compiler defines this. Testing it is equivalent to testing (__GNUC__ && __cplusplus).

__STRICT_ANSI__

GCC defines this macro if and only if the -ansi switch, or a -std switch specifying strict conformance to some version of ISO C or ISO C++, was specified when GCC was invoked. It is defined to ‘1’. This macro exists primarily to direct GNU libc's header files to restrict their definitions to the minimal set found in the 1989 C standard.

__BASE_FILE__

This macro expands to the name of the main input file, in the form of a C string constant. This is the source file that was specified on the command line of the preprocessor or C compiler.

__INCLUDE_LEVEL__

This macro expands to a decimal integer constant that represents the depth of nesting in include files. The value of this macro is incremented on every ‘#include’ directive and decremented at the end of every included file. It starts out at 0, its value within the base file specified on the command line.

__ELF__

This macro is defined if the target uses the ELF object format.

__VERSION__

This macro expands to a string constant which describes the version of the compiler in use. You should not rely on its contents having any particular form, but it can be counted on to contain at least the release number.

__OPTIMIZE__

__OPTIMIZE_SIZE__

__NO_INLINE__

These macros describe the compilation mode. __OPTIMIZE__ is defined in all optimizing compilations. __OPTIMIZE_SIZE__ is defined if the compiler is optimizing for size, not speed. __NO_INLINE__ is defined if no functions will be inlined into their callers (when not optimizing, or when inlining has been specifically disabled by -fno-inline).

These macros cause certain GNU header files to provide optimized definitions, using macros or inline functions, of system library functions. You should not use these macros in any way unless you make sure that programs will execute with the same effect whether or not they are defined. If they are defined, their value is 1.



__GNUC_GNU_INLINE__

GCC defines this macro if functions declared inline will be handled in GCC's traditional gnu90 mode. Object files will contain externally visible definitions of all functions declared inline without extern or static. They will not contain any definitions of any functions declared extern inline.

__GNUC_STDC_INLINE__

GCC defines this macro if functions declared inline will be handled according to the ISO C99 standard. Object files will contain externally visible definitions of all functions declared extern inline. They will not contain definitions of any functions declared inline without extern.

If this macro is defined, GCC supports the gnu_inline function attribute as a way to always get the gnu90 behavior. Support for this and __GNUC_GNU_INLINE__ was added in GCC 4.1.3. If neither macro is defined, an older version of GCC is being used: inline functions will be compiled in gnu90 mode, and the gnu_inline function attribute will not be recognized.



__CHAR_UNSIGNED__

GCC defines this macro if and only if the data type char is unsigned on the target machine. It exists to cause the standard header file limits.h to work correctly. You should not use this macro yourself; instead, refer to the standard macros defined in limits.h.

__WCHAR_UNSIGNED__

Like __CHAR_UNSIGNED__, this macro is defined if and only if the data type wchar_t is unsigned and the front-end is in C++ mode.

__REGISTER_PREFIX__

This macro expands to a single token (not a string constant) which is the prefix applied to CPU register names in assembly language for this target. You can use it to write assembly that is usable in multiple environments. For example, in the m68k-aout environment it expands to nothing, but in the m68k-coff environment it expands to a single ‘%’.

__USER_LABEL_PREFIX__

This macro expands to a single token which is the prefix applied to user labels (symbols visible to C code) in assembly. For example, in the m68k-aout environment it expands to an ‘_’, but in the m68k-coff environment it expands to nothing.

This macro will have the correct definition even if -f(no-)underscores is in use, but it will not be correct if target-specific options that adjust this prefix are used (e.g. the OSF/rose -mno-underscores option).
