AC_PREREQ ( [ 2.69 ] )
define ( _CLIENT_VERSION_MAJOR , 0 )
определить ( _CLIENT_VERSION_MINOR , 19 )
определить ( _CLIENT_VERSION_REVISION , 99 )
define ( _CLIENT_VERSION_BUILD , 0 )
определить ( _CLIENT_VERSION_RC , 0 )
определить ( _CLIENT_VERSION_IS_RELEASE , ложь )
определить ( _COPYRIGHT_YEAR , 2020 )
define ( _COPYRIGHT_HOLDERS , [ Разработчики% s ] )
define ( _COPYRIGHT_HOLDERS_SUBSTITUTION , [ [ Биткойн-ядро ] ] )
AC_INIT ( [ Биткойн Ядро ] , m4_join ( [ . ] , _CLIENT_VERSION_MAJOR , _CLIENT_VERSION_MINOR , _CLIENT_VERSION_REVISION , m4_if ( _CLIENT_VERSION_BUILD , [ 0 ] , [ ] , _CLIENT_VERSION_BUILD ) ) m4_if ( _CLIENT_VERSION_RC , [ 0 ] , [ ] , [ RC ] _CLIENT_VERSION_RC ), [ https://github.com/bitcoin/bitcoin/issues ] , [ bitcoin ] , [ https://bitcoincore.org/ ] )
AC_CONFIG_SRCDIR ( [ src / validation.cpp ] )
AC_CONFIG_HEADERS ( [ src / config / bitcoin-config.h ] )
AC_CONFIG_AUX_DIR ( [ build-aux ] )
AC_CONFIG_MACRO_DIR ( [ build-aux / m4 ] )

BITCOIN_DAEMON_NAME = bitcoind
BITCOIN_GUI_NAME = Bitcoin-кварта
BITCOIN_CLI_NAME = Bitcoin-кли
BITCOIN_TX_NAME = Bitcoin-TX
BITCOIN_WALLET_TOOL_NAME = Bitcoin-кошелек

dnl Если пользователь не указал ARFLAGS, заставь его взломать
AC_ARG_VAR ( ARFLAGS , [ Флаги для архиватора, по умолчанию <cr>, если не установлен ] )
if test "x $ {ARFLAGS + set}"! = "xset"; тогда
  ARFLAGS = "кр"
фи

макрос AC_CANONICAL_HOST

AH_TOP ( [ #ifndef BITCOIN_CONFIG_H ] )
AH_TOP ( [ #define BITCOIN_CONFIG_H ] )
AH_BOTTOM ( [ #endif // BITCOIN_CONFIG_H ] )

dnl faketime breaks настроить и нужен только для make. Отключи это здесь.
сбросить ФАКЕТИМ

dnl Automake инициализация установки и проверки
AM_INIT_AUTOMAKE ( [ внешние объекты без определения subdir ] )

dnl faketime портит временные метки и приводит к повторному запуску configure.
dnl --disable- keeper -mode может использоваться для обхода этого.
AM_MAINTAINER_MODE ( [ включить ] )

dnl делает флаги компиляции тихими, если не используется V = 1
m4_ifdef ( [ AM_SILENT_RULES ] , [ AM_SILENT_RULES ( [ да ] ) ] )

dnl Компилятор проверяет (здесь до libtool).
if test "x $ {CXXFLAGS + set}" = "xset"; тогда
  CXXFLAGS_overridden = да
еще
  CXXFLAGS_overridden = нет
фи
AC_PROG_CXX

dnl По умолчанию libtool для mingw отказывается связывать статические библиотеки в dll для
dnl боязнь смешивать объекты pic / non-pic и сложности импорта / экспорта. поскольку
У нас все под контролем, включите эту функцию.
case $ host in
  * MinGW *)
     lt_cv_deplibs_check_method = "pass_all"
  ;;
ESAC
dnl Требуется компилятор C ++ 11 (без расширений GNU)
AX_CXX_COMPILE_STDCXX ( [ 11 ] , [ noext ] , [ обязательный ] , [ nodefault ] )
dnl Проверить, требуется ли -latomic для <std :: atomic>
CHECK_ATOMIC

dnl Если пользователь не указал OBJCXX, заставьте его быть таким же, как CXX. Это обеспечивает
dnl, что мы получаем одинаковые флаги -std для обоих.
m4_ifdef ( [ AC_PROG_OBJCXX ] , [
if test "x $ {OBJCXX + set}" = "x"; тогда
  OBJCXX = "$ {CXX}"
фи
AC_PROG_OBJCXX
] )

dnl Начиная с libtool 1.5.2 (выпущена 2004-01-25), в Linux libtool больше нет
dnl устанавливает RPATH для любых каталогов в пути поиска динамического компоновщика.
dnl Подробнее: https://wiki.debian.org/RpathIssue
LT_PREREQ ( [ 1.5.2 ] )
dnl Libtool init проверяет.
LT_INIT ( [ только изображение ] )

dnl Проверка / возврат PATH для базовых программ.
AC_PATH_TOOL ( AR , ar )
AC_PATH_TOOL ( RANLIB , ranlib )
AC_PATH_TOOL ( STRIP , полоса )
AC_PATH_TOOL ( GCOV , gcov )
AC_PATH_PROG ( LCOV , lcov )
dnl Python 3.5 указан в .python-версии и должен использоваться, если он доступен, см. doc / dependencies.md
AC_PATH_PROGS ( [ PYTHON ] , [ python3.5 python3.6 python3.7 python3.8 python3 python ] )
AC_PATH_PROG ( GENHTML , genhtml )
AC_PATH_PROG ( [ GIT ] , [ git ] )
AC_PATH_PROG ( CCache , CCache )
AC_PATH_PROG ( XGETTEXT , xgettext )
AC_PATH_PROG ( HexDump , шестнадцатеричный )
AC_PATH_TOOL ( READELF , readelf )
AC_PATH_TOOL ( CPPFILT , с ++ фильт )
AC_PATH_TOOL ( OBJCOPY , objcopy )
AC_PATH_PROG ( DOXYGEN , doxygen )
if test -z "$ DOXYGEN"; тогда
   AC_MSG_WARN ( [ Doxygen не найден ] )
фи
AM_CONDITIONAL ( [ HAVE_DOXYGEN ] , [ test -n "$ DOXYGEN" ] )

AC_ARG_VAR ( PYTHONPATH , увеличивает  путь поиска по  умолчанию  для файлов модулей Python )     

AC_ARG_ENABLE ( [ кошелек ] ,
  [ AS_HELP_STRING ( [ --disable-кошелек ] ,
  [ отключить кошелек (включен по умолчанию) ] ) ] ,
  [ enable_wallet = $ enableval ] ,
  [ enable_wallet = yes ] )

AC_ARG_WITH ( [ miniupnpc ] ,
  [ AS_HELP_STRING ( [ --with-miniupnpc ] ,
  [ включить UPNP (по умолчанию да, если libminiupnpc найден) ] ) ] ,
  [ use_upnp = $ withval ] ,
  [ use_upnp = auto ] )

AC_ARG_ENABLE ( [ upnp-default ] ,
  [ AS_HELP_STRING ( [ --enable-upnp-default ] ,
  [ если UPNP включен, включите его при запуске (по умолчанию нет) ] ) ] ,
  [ use_upnp_default = $ enableval ] ,
  [ use_upnp_default = no ] )

AC_ARG_ENABLE ( тесты ,
    AS_HELP_STRING ( [ --disable-tests ] , [ не компилировать тесты (по умолчанию компилирование) ] ) ,
    [ use_tests = $ enableval ] ,
    [ use_tests = yes ] )

AC_ARG_ENABLE ( графические тесты ,
    AS_HELP_STRING ( [ --disable-gui-tests ] , [ не компилировать тесты GUI (по умолчанию компилируется, если GUI и тесты включены) ] ) ,
    [ use_gui_tests = $ enableval ] ,
    [ use_gui_tests = $ use_tests ] )

AC_ARG_WITH ( [ экспресс-проверка ] ,
  [ AS_HELP_STRING ( [ --with-rapidcheck ] ,
  [ Включить RapidCheck свойств на основе тестов ( по умолчанию это да , если librapidcheck найден) ] ) ] ,
  [ use_rapidcheck = $ withval ] ,
  [ use_rapidcheck = auto ] )

AC_ARG_ENABLE ( скамейка ,
    AS_HELP_STRING ( [ --disable-bench ] , [ не компилировать тесты (по умолчанию компилировать) ] ) ,
    [ use_bench = $ enableval ] ,
    [ use_bench = yes ] )

AC_ARG_ENABLE ( [ расширенные-функциональные-тесты ] ,
    AS_HELP_STRING ( [ --enable-extended-functions-tests ] , [ включить дорогостоящие функциональные тесты при использовании lcov (по умолчанию no) ] ) ,
    [ use_extended_functional_tests = $ enableval ] ,
    [ use_extended_functional_tests = no ] )

AC_ARG_ENABLE ( [ fuzz ] ,
    AS_HELP_STRING ( [ --enable-fuzz ] ,
    [ Не позволит построить из пуха целей ( по умолчанию нет). включение этого отключит все другие цели ] ) ,
    [ enable_fuzz = $ enableval ] ,
    [ enable_fuzz = no ] )

AC_ARG_WITH ( [ qrencode ] ,
  [ AS_HELP_STRING ( [ --with-qrencode ] ,
  [ включить поддержку QR-кода (по умолчанию да, если включен qt и найден libqrencode) ] ) ] ,
  [ use_qr = $ withval ] ,
  [ use_qr = auto ] )

AC_ARG_ENABLE ( [ закаливание ] ,
  [ AS_HELP_STRING ( [ --disable- hardening ] ,
  [ не пытайтесь укрепить получившиеся исполняемые файлы (по умолчанию это усиление, когда это возможно) ] ) ] ,
  [ use_hardening = $ enableval ] ,
  [ use_hardening = auto ] )

AC_ARG_ENABLE ( [ уменьшить-экспорт ] ,
  [ AS_HELP_STRING ( [ --enable- redu-export ] ,
  [ попытка уменьшить экспортируемые символы в результирующих исполняемых файлах (по умолчанию нет) ] ) ] ,
  [ use_reduce_exports = $ enableval ] ,
  [ use_reduce_exports = no ] )

AC_ARG_ENABLE ( [ ccache ] ,
  [ AS_HELP_STRING ( [ --disable-ccache ] ,
  [ не используйте ccache для сборки (по умолчанию используется, если найдено) ] ) ] ,
  [ use_ccache = $ enableval ] ,
  [ use_ccache = auto ] )

AC_ARG_ENABLE ( [ lcov ] ,
  [ AS_HELP_STRING ( [ --enable-lcov ] ,
  [ включить тестирование lcov (по умолчанию нет) ] ) ] ,
  [ use_lcov = $ enableval ] ,
  [ use_lcov = no ] )

AC_ARG_ENABLE ( [ lcov-branch-покрытие ] ,
  [ AS_HELP_STRING ( [ --enable-lcov-branch-покрытие ] ,
  [ Включить освещение филиального тестирования lcov ( по умолчанию нет) ] ) ] ,
  [ use_lcov_branch = yes ] ,
  [ use_lcov_branch = no ] )

AC_ARG_ENABLE ( [ glibc-back-compat ] ,
  [ AS_HELP_STRING ( [ --enable-glibc-back-compat ] ,
  [ включить обратную совместимость с glibc ] ) ] ,
  [ use_glibc_compat = $ enableval ] ,
  [ use_glibc_compat = no ] )

AC_ARG_ENABLE ( [ threadlocal ] ,
  [ AS_HELP_STRING ( [ --enable-threadlocal ] ,
  [ Включить функции , которые зависят от C ++ thread_local ключевого слова ( в настоящее время только нитку имен в журналах отладки). (по умолчанию включено, если есть поддержка платформы и glibc-back-compat не включен) ] ) ] ,
  [ use_thread_local = $ enableval ] ,
  [ use_thread_local = auto ] )

AC_ARG_ENABLE ( [ asm ] ,
  [ AS_HELP_STRING ( [ --disable-asm ] ,
  [ отключить процедуры сборки (по умолчанию включено) ] ) ] ,
  [ use_asm = $ enableval ] ,
  [ use_asm = yes ] )

if test "x $ use_asm" = xyes; тогда
  AC_DEFINE ( USE_ASM , 1 , [ определить этот символ для встраивания в процедуры сборки ] )
фи

AC_ARG_WITH ( [ системный однозначный номер ] ,
  [ AS_HELP_STRING ( [ --with-system-univalue ] ,
  [ Сборка с системой UniValue (по умолчанию нет) ] ) ] ,
  [ system_univalue = $ withval ] ,
  [ system_univalue = нет ]
)
AC_ARG_ENABLE ( [ zmq ] ,
  [ AS_HELP_STRING ( [ --disable-zmq ] ,
  [ отключить уведомления ZMQ ] ) ] ,
  [ use_zmq = $ enableval ] ,
  [ use_zmq = yes ] )

AC_ARG_ENABLE ( [ bip70 ] ,
  [ AS_HELP_STRING ( [ --enable-bip70 ] ,
  [ Поддержка BIP70 (платежный протокол) в графическом интерфейсе (больше не поддерживается) ] ) ] ,
  [ enable_bip70 = $ enableval ] ,
  [ enable_bip70 = нет ] )

if test x $ enable_bip70! = xno; тогда
  AC_MSG_ERROR ( [ BIP70 больше не поддерживается! ] )
фи

AC_ARG_ENABLE ( мужчина ,
    [ AS_HELP_STRING ( [ --disable-man ] ,
                    [ не устанавливайте man-страницы (по умолчанию устанавливается) ] ) ] ,,
    enable_man = да )
AM_CONDITIONAL (ENABLE_MAN, тест "$ enable_man"! = Нет)

dnl включить отладку
AC_ARG_ENABLE ( [ отладка ] ,
    [ AS_HELP_STRING ( [ --enable-debug ] ,
                    [ Использование флаги компилятора и макросы , подходящие для отладки ( по умолчанию нет) ] ) ] ,
    [ enable_debug = $ enableval ] ,
    [ enable_debug = no ] )

dnl Включить разные опции -fsanitize
AC_ARG_WITH ( [ дезинфицирующие средства ] ,
    [ AS_HELP_STRING ( [ --with-sanitizers ] ,
                    [ разделенный запятыми список дополнительных дезинфицирующих средств для сборки (по умолчанию ни один не включен) ] ) ] ,
    [ use_sanitizers = $ withval ] )

dnl включить профилирование gprof
AC_ARG_ENABLE ( [ gprof ] ,
    [ AS_HELP_STRING ( [ --enable-gprof ] ,
                    [ Использование дргоГо профилирования флаги компилятора ( по умолчанию нет) ] ) ] ,
    [ enable_gprof = $ enableval ] ,
    [ enable_gprof = no ] )

dnl превратить предупреждения в ошибки
AC_ARG_ENABLE ( [ ошибка ] ,
    [ AS_HELP_STRING ( [ --enable-werror ] ,
                    [ Лечить некоторые предупреждения компилятора как ошибки ( по умолчанию нет) ] ) ] ,
    [ enable_werror = $ enableval ] ,
    [ enable_werror = no ] )

AC_LANG_PUSH ( [ C ++ ] )
AX_CHECK_COMPILE_FLAG ( [ -Werror ] , [ CXXFLAG_WERROR = "- Werror" ] , [ CXXFLAG_WERROR = "" ] )

if test "x $ enable_debug" = xyes; тогда
  dnl Очистить флаги по умолчанию -g -O2
  if test "x $ CXXFLAGS_overridden" = xno; тогда
	CXXFLAGS = ""
  фи

  DnL Отключить все оптимизации
  AX_CHECK_COMPILE_FLAG ( [ -O0 ] , [ [ DEBUG_CXXFLAGS = "$ DEBUG_CXXFLAGS -O0" ] ] ,, [ [ $ CXXFLAG_WERROR ] ] )

  dnl Предпочитают -g3, возвращайтесь к -g, если это недоступно.
  AX_CHECK_COMPILE_FLAG (
    [ -g3 ] ,
    [ [ DEBUG_CXXFLAGS = "$ DEBUG_CXXFLAGS -g3" ] ] ,
    [ AX_CHECK_COMPILE_FLAG ( [ -g ] , [ [ DEBUG_CXXFLAGS = "$ DEBUG_CXXFLAGS -g" ] ] ,, [ [ $ CXXFLAG_WERROR ] ] ) ] ,
    [ [ $ CXXFLAG_WERROR ] ] )

  AX_CHECK_PREPROC_FLAG ( [ -DDEBUG ] , [ [ DEBUG_CPPFLAGS = "$ DEBUG_CPPFLAGS -DDEBUG" ] ] ,, [ [ $ CXXFLAG_WERROR ] ] )
  AX_CHECK_PREPROC_FLAG ( [ -DDEBUG_LOCKORDER ] , [ [ DEBUG_CPPFLAGS = "$ DEBUG_CPPFLAGS -DDEBUG_LOCKORDER" ] ] ,, [ [ $ CXXFLAG_WERROR ] ] )
  AX_CHECK_COMPILE_FLAG ( [ -ftrapv ] , [ DEBUG_CXXFLAGS = "$ DEBUG_CXXFLAGS -ftrapv" ] ,, [ [ $ CXXFLAG_WERROR ] ] )
фи

if test x $ use_sanitizers! = x; тогда
  DNL Сначала проверьте , если компилятор принимает флаги. Если несовместимая пара, как
  dnl -fsanitize = адрес, здесь используется нить, эта проверка не будет выполнена. Это также
  Ошибка dnl, если передан неверный аргумент, например -fsanitize = undefeined
  AX_CHECK_COMPILE_FLAG (
    [ [ -fsanitize = $ use_sanitizers ] ] ,
    [ [ SANITIZER_CXXFLAGS = -fsanitize = $ use_sanitizers ] ] ,
    [ AC_MSG_ERROR ( [ компилятор не принял запрошенные флаги ] ) ] )

  DnL Некоторые компиляторы (например , GCC) требует дополнительных библиотек , как libasan,
  dnl libtsan, libubsan и т. д. Убедитесь, что связывание все еще работает с sanitize
  флаг dnl . Это отдельная проверка, поэтому мы можем дать лучшее сообщение об ошибке, когда
  dnl флаги sanitize поддерживаются компилятором, но фактическим sanitizer
  DNL библиотеки отсутствуют.
  AX_CHECK_LINK_FLAG (
    [ [ -fsanitize = $ use_sanitizers ] ] ,
    [ [ SANITIZER_LDFLAGS = -fsanitize = $ use_sanitizers ] ] ,
    [ AC_MSG_ERROR ( [ компоновщик не принял запрошенные флаги, у вас отсутствуют обязательные библиотеки ] ) ] ,
    [ ] ,
    [ AC_LANG_PROGRAM ( [ [
    #include <cstdint>
    #include <cstddef>
    extern "C" int LLVMFuzzerTestOneInput (const uint8_t * data, size_t size) {return 0; }
    __attribute __ ((слабый)) // разрешить связывание libFuzzer
    ] ] , [ [ ] ] )])
фи

ERROR_CXXFLAGS =
if test "x $ enable_werror" = "xyes"; тогда
  if test "x $ CXXFLAG_WERROR" = "x"; тогда
    AC_MSG_ERROR ( "включить-werror  набор ,  но  - Werror  это  не  использовать" )
  фи
  AX_CHECK_COMPILE_FLAG ( [ -Werror = vla ] , [ ERROR_CXXFLAGS = "$ ERROR_CXXFLAGS -Werror = vla" ] ,, [ [ $ CXXFLAG_WERROR ] ] )
  AX_CHECK_COMPILE_FLAG ( [ -Werror = switch ] , [ ERROR_CXXFLAGS = "$ ERROR_CXXFLAGS -Werror = switch" ] ,, [ [ $ CXXFLAG_WERROR ] ] )
  AX_CHECK_COMPILE_FLAG ( [ -Werror = анализ безопасности потока ] , [ ERROR_CXXFLAGS = "$ ERROR_CXXFLAGS -Werror = анализ безопасности потока" ] ,, [ [ $ CXXFLAG_WERROR ] ] )
  AX_CHECK_COMPILE_FLAG ( [ -Werror = unused-variable ] , [ ERROR_CXXFLAGS = "$ ERROR_CXXFLAGS -Werror = unused-variable" ] ,, [ [ $ CXXFLAG_WERROR ] ] )
  AX_CHECK_COMPILE_FLAG ( [ -Werror = дата-время ] , [ ERROR_CXXFLAGS = "$ ERROR_CXXFLAGS -Werror = дата-время" ] ,, [ [ $ CXXFLAG_WERROR ] ] )
фи

if test "x $ CXXFLAGS_overridden" = "xno"; тогда
  AX_CHECK_COMPILE_FLAG ( [ -Wall ] , [ WARN_CXXFLAGS = "$ WARN_CXXFLAGS -Wall" ] ,, [ [ $ CXXFLAG_WERROR ] ] )
  AX_CHECK_COMPILE_FLAG ( [ -Wextra ] , [ WARN_CXXFLAGS = "$ WARN_CXXFLAGS -Wextra" ] ,, [ [ $ CXXFLAG_WERROR ] ] )
  AX_CHECK_COMPILE_FLAG ( [ -Wformat ] , [ WARN_CXXFLAGS = "$ WARN_CXXFLAGS -Wformat" ] ,, [ [ $ CXXFLAG_WERROR ] ] )
  AX_CHECK_COMPILE_FLAG ( [ -Wvla ] , [ WARN_CXXFLAGS = "$ WARN_CXXFLAGS -Wvla" ] ,, [ [ $ CXXFLAG_WERROR ] ] )
  AX_CHECK_COMPILE_FLAG ( [ -Wswitch ] , [ WARN_CXXFLAGS = "$ WARN_CXXFLAGS -Wswitch" ] ,, [ [ $ CXXFLAG_WERROR ] ] )
  AX_CHECK_COMPILE_FLAG ( [ -Wformat-security ] , [ WARN_CXXFLAGS = "$ WARN_CXXFLAGS -Wformat-security" ] ,, [ [ $ CXXFLAG_WERROR ] ] )
  AX_CHECK_COMPILE_FLAG ( [ -Wread-анализ безопасности ] , [ WARN_CXXFLAGS = "$ WARN_CXXFLAGS -Wread-safety-analysis" ] ,, [ [ $ CXXFLAG_WERROR ] ] )
  AX_CHECK_COMPILE_FLAG ( [ -Wrange-loop-analysis ] , [ WARN_CXXFLAGS = "$ WARN_CXXFLAGS -Wrange-loop-analysis" ] ,, [ [ $ CXXFLAG_WERROR ] ] )
  AX_CHECK_COMPILE_FLAG ( [ -Wredundant-decls ] , [ WARN_CXXFLAGS = "$ WARN_CXXFLAGS -Wredundant-decls" ] ,, [ [ $ CXXFLAG_WERROR ] ] )
  AX_CHECK_COMPILE_FLAG ( [ -Wunused-variable ] , [ WARN_CXXFLAGS = "$ WARN_CXXFLAGS -Wunused-variable" ] ,, [ [ $ CXXFLAG_WERROR ] ] )
  AX_CHECK_COMPILE_FLAG ( [ -Wdate-time ] , [ WARN_CXXFLAGS = "$ WARN_CXXFLAGS -Wdate-time" ] ,, [ [ $ CXXFLAG_WERROR ] ] )

  dnl Некоторые компиляторы (gcc) игнорируют неизвестные опции -Wno- *, но предупреждают обо всех
  Неизвестные опции, если выдается другое предупреждение. Проверьте случай -Wfoo и
  dnl устанавливает случай -Wno-foo, если он работает.
  AX_CHECK_COMPILE_FLAG ( [ -Wunused-параметр ] , [ NOWARN_CXXFLAGS = "$ NOWARN_CXXFLAGS -Wno-unused-параметр" ] ,, [ [ $ CXXFLAG_WERROR ] ] )
  AX_CHECK_COMPILE_FLAG ( [ -Wself-assign ] , [ NOWARN_CXXFLAGS = "$ NOWARN_CXXFLAGS -Wno-self-assignment" ] ,, [ [ $ CXXFLAG_WERROR ] ] )
  AX_CHECK_COMPILE_FLAG ( [ -Wunused-local-typedef ] , [ NOWARN_CXXFLAGS = "$ NOWARN_CXXFLAGS -Wno-unused-local-typedef" ] ,, [ [ $ CXXFLAG_WERROR ] ] )
  AX_CHECK_COMPILE_FLAG ( [ -Wdeprecated-register ] , [ NOWARN_CXXFLAGS = "$ NOWARN_CXXFLAGS -Wno-deprecated-register" ] ,, [ [ $ CXXFLAG_WERROR ] ] )
  AX_CHECK_COMPILE_FLAG ( [ -Wimplicit-fallthrough ] , [ NOWARN_CXXFLAGS = "$ NOWARN_CXXFLAGS -Wno-implicit-fallthrough" ] ,, [ [ $ CXXFLAG_WERROR ] ] )
фи

enable_hwcrc32 = нет
enable_sse41 = нет
enable_avx2 = нет
enable_shani = нет

if test "x $ use_asm" = "xyes"; тогда

dnl Проверьте наличие дополнительной поддержки набора команд. Включение этого не означает, что весь код будет
dnl должен быть скомпилирован с ними, а определенные объекты / библиотеки могут использовать их после проверки на время выполнения
dnl совместимость
AX_CHECK_COMPILE_FLAG ( [ -msse4.2 ] , [ [ SSE42_CXXFLAGS = "- msse4.2" ] ] ,, [ [ $ CXXFLAG_WERROR ] ] )
AX_CHECK_COMPILE_FLAG ( [ -msse4.1 ] , [ [ SSE41_CXXFLAGS = "- msse4.1" ] ] ,, [ [ $ CXXFLAG_WERROR ] ] )
AX_CHECK_COMPILE_FLAG ( [ -mavx -mavx2 ] , [ [ AVX2_CXXFLAGS = "- mavx -mavx2" ] ] ,, [ [ $ CXXFLAG_WERROR ] ] )
AX_CHECK_COMPILE_FLAG ( [ -msse4 -msha ] , [ [ SHANI_CXXFLAGS = "- msse4 -msha" ] ] ,, [ [ $ CXXFLAG_WERROR ] ] )

TEMP_CXXFLAGS = "$ CXXFLAGS"
CXXFLAGS = "$ CXXFLAGS $ SSE42_CXXFLAGS"
AC_MSG_CHECKING ( для  поддержки ассемблера  crc32  )
AC_COMPILE_IFELSE ( [ AC_LANG_PROGRAM ( [ [
    #include <stdint.h>
    #iffined (_MSC_VER)
    #include <intrin.h>
    #elif определен (__ GNUC__) && определен (__ SSE4_2__)
    #include <nmmintrin.h>
    #endif
  ] ] , [ [
    uint64_t l = 0;
    l = _mm_crc32_u8 (l, 0);
    l = _mm_crc32_u32 (l, 0);
    l = _mm_crc32_u64 (l, 0);
    возврат л;
  ] ] )],
 [  AC_MSG_RESULT ( да ) ; enable_hwcrc32 = yes ] ,
 [  AC_MSG_RESULT ( нет ) ]
)
CXXFLAGS = "$ TEMP_CXXFLAGS"

TEMP_CXXFLAGS = "$ CXXFLAGS"
CXXFLAGS = "$ CXXFLAGS $ SSE41_CXXFLAGS"
AC_MSG_CHECKING ( для  встроенных функций SSE4.1  )
AC_COMPILE_IFELSE ( [ AC_LANG_PROGRAM ( [ [
    #include <stdint.h>
    #include <immintrin.h>
  ] ] , [ [
    __m128i l = _mm_set1_epi32 (0);
    return _mm_extract_epi32 (l, 3);
  ] ] )],
 [  AC_MSG_RESULT ( да ) ; enable_sse41 = да; AC_DEFINE ( ENABLE_SSE41 , 1 , [ Определить этот символ для построения кода, который использует встроенные функции SSE4.1 ] )  ] ,
 [  AC_MSG_RESULT ( нет ) ]
)
CXXFLAGS = "$ TEMP_CXXFLAGS"

TEMP_CXXFLAGS = "$ CXXFLAGS"
CXXFLAGS = "$ CXXFLAGS $ AVX2_CXXFLAGS"
AC_MSG_CHECKING ( для  встроенных функций AVX2  )
AC_COMPILE_IFELSE ( [ AC_LANG_PROGRAM ( [ [
    #include <stdint.h>
    #include <immintrin.h>
  ] ] , [ [
    __m256i l = _mm256_set1_epi32 (0);
    return _mm256_extract_epi32 (l, 7);
  ] ] )],
 [  AC_MSG_RESULT ( да ) ; enable_avx2 = да; AC_DEFINE ( ENABLE_AVX2 , 1 , [ Определить этот символ для построения кода, который использует встроенные функции AVX2 ] )  ] ,
 [  AC_MSG_RESULT ( нет ) ]
)
CXXFLAGS = "$ TEMP_CXXFLAGS"

TEMP_CXXFLAGS = "$ CXXFLAGS"
CXXFLAGS = "$ CXXFLAGS $ SHANI_CXXFLAGS"
AC_MSG_CHECKING ( для  встроенных функций SHA-NI  )
AC_COMPILE_IFELSE ( [ AC_LANG_PROGRAM ( [ [
    #include <stdint.h>
    #include <immintrin.h>
  ] ] , [ [
    __m128i i = _mm_set1_epi32 (0);
    __m128i j = _mm_set1_epi32 (1);
    __m128i k = _mm_set1_epi32 (2);
    return _mm_extract_epi32 (_mm_sha256rnds2_epu32 (i, i, k), 0);
  ] ] )],
 [  AC_MSG_RESULT ( да ) ; enable_shani = да; AC_DEFINE ( ENABLE_SHANI , 1 , [ Определить этот символ для построения кода, который использует встроенные функции SHA-NI ] )  ] ,
 [  AC_MSG_RESULT ( нет ) ]
)
CXXFLAGS = "$ TEMP_CXXFLAGS"

фи

CPPFLAGS = "$ CPPFLAGS -DHAVE_BUILD_INFO -D__STDC_FORMAT_MACROS"

AC_ARG_WITH ( [ utils ] ,
  [ AS_HELP_STRING ( [ --with-utils ] ,
  [ build bitcoin-cli bitcoin-tx биткойн-кошелек (по умолчанию = да) ] ) ] ,
  [ build_bitcoin_utils = $ withval ] ,
  [ build_bitcoin_utils = yes ] )

AC_ARG_ENABLE ( [ util-cli ] ,
  [ AS_HELP_STRING ( [ --enable-util-cli ] ,
  [ Сборка Bitcoin-кли ] ) ] ,
  [ build_bitcoin_cli = $ enableval ] ,
  [ build_bitcoin_cli = $ build_bitcoin_utils ] )

AC_ARG_ENABLE ( [ util-tx ] ,
  [ AS_HELP_STRING ( [ --enable-util-tx ] ,
  [ build bitcoin-tx ] ) ] ,
  [ build_bitcoin_tx = $ enableval ] ,
  [ build_bitcoin_tx = $ build_bitcoin_utils ] )

AC_ARG_ENABLE ( [ утилитный кошелек ] ,
  [ AS_HELP_STRING ( [ --enable-util-wallet ] ,
  [ построить биткойн-кошелек ] ) ] ,
  [ build_bitcoin_wallet = $ enableval ] ,
  [ build_bitcoin_wallet = $ build_bitcoin_utils ] )

AC_ARG_WITH ( [ libs ] ,
  [ AS_HELP_STRING ( [ --with-libs ] ,
  [ сборка библиотек (по умолчанию = да) ] ) ] ,
  [ build_bitcoin_libs = $ withval ] ,
  [ build_bitcoin_libs = yes ] )

AC_ARG_WITH ( [ демон ] ,
  [ AS_HELP_STRING ( [ --with-daemon ] ,
  [ build bitcoind daemon (по умолчанию = yes) ] ) ] ,
  [ build_bitcoind = $ withval ] ,
  [ build_bitcoind = yes ] )

use_pkgconfig = да
case $ host in
  * MinGW *)

     dnl pkgconfig приносит больше вреда, чем пользы с MinGW
     = use_pkgconfig нет

     TARGET_OS = окна
     AC_CHECK_LIB ( [ kernel32 ] , [ GetModuleFileNameA ] ,, AC_MSG_ERROR ( отсутствует libkernel32  ) )
     AC_CHECK_LIB ( [ user32 ] ,    [ main ] ,, AC_MSG_ERROR ( отсутствует libuser32  ) )
     AC_CHECK_LIB ( [ gdi32 ] ,     [ main ] ,, AC_MSG_ERROR ( отсутствует libgdi32  ) )
     AC_CHECK_LIB ( [ comdlg32 ] , [ main ] ,, AC_MSG_ERROR ( отсутствует libcomdlg32  ) )
     AC_CHECK_LIB ( [ winmm ] ,     [ main ] ,, AC_MSG_ERROR ( отсутствует libwinmm  ) )
     AC_CHECK_LIB ( [ shell32 ] ,   [ SHGetSpecialFolderPathW ] ,, AC_MSG_ERROR ( libshell32  отсутствует ) )
     AC_CHECK_LIB ( [ comctl32 ] , [ main ] ,, AC_MSG_ERROR ( отсутствует libcomctl32  ) )
     AC_CHECK_LIB ( [ ole32 ] ,     [ CoCreateInstance ] ,, AC_MSG_ERROR ( libole32  отсутствует ) )
     AC_CHECK_LIB ( [ oleaut32 ] , [ main ] ,, AC_MSG_ERROR ( liboleaut32  отсутствует ) )
     AC_CHECK_LIB ( [ uuid ] ,      [ main ] ,, AC_MSG_ERROR ( отсутствует libuuid  ) )
     AC_CHECK_LIB ( [ advapi32 ] , [ CryptAcquireContextW ] , AC_MSG_ERROR ( отсутствует libadvapi32  ) )
     AC_CHECK_LIB ( [ ws2_32 ] ,    [ WSAStartup ] , AC_MSG_ERROR ( отсутствует libws2_32  ) )
     AC_CHECK_LIB ( [ shlwapi ] ,   [ PathRemoveFileSpecW ] , AC_MSG_ERROR ( libshlwapi  отсутствует ) )
     AC_CHECK_LIB ( [ iphlpapi ] , [ GetAdaptersAddresses ] ,, AC_MSG_ERROR ( отсутствует libiphlpapi  ) )

     dnl -static интерпретируется libtool, где имеет другое значение.
     DNL В Libtool -говорить, это -все-статичным.
     AX_CHECK_LINK_FLAG ( [ [ -static ] ] , [ LIBTOOL_APP_LDFLAGS = "$ LIBTOOL_APP_LDFLAGS -all-static" ] )

     AC_PATH_PROG ( [ MAKENSIS ] , [ makensis ] , нет )
     if test x $ MAKENSIS = xnone; тогда
       AC_MSG_WARN ( "makensis  не  найден.  Не  удается создать  установщик." )
     фи

     AC_PATH_TOOL ( WINDRES , windres , нет )
     if test x $ WINDRES = xnone; тогда
       AC_MSG_ERROR ( "windres  not  found" )
     фи

     CPPFLAGS = "$ CPPFLAGS -D_MT -DWIN32 -D_WINDOWS -DBOOST_THREAD_USE_LIB -D_WIN32_WINNT = 0x0601"
     LEVELDB_TARGET_FLAGS = "- DOS_WINDOWS"
     if test "x $ CXXFLAGS_overridden" = "xno"; тогда
       CXXFLAGS = "$ CXXFLAGS -w"
     фи

     dnl libtool настаивает на добавлении -nostdlib и списка объектов / библиотек для ссылки.
     dnl Это нарушает нашу способность создавать dll с помощью статических libgcc / libstdc ++ / libssp. Override
     dnl его команда здесь, с удаленными preps / postdeps и вставкой -static. Постдепс
     dnl также переопределяется, чтобы предотвратить их вставку позже.
     DNL Это должно повлиять только библиотеки DLL.
     archive_cmds_CXX = "\ $ CC -shared \ $ libobjs \ $ deplibs \ $ compiler_flags -static -o \ $ output_objdir / \ $ soname \ $ {wl} - enable-auto-image-base -Xlinker --out-implib - Xlinker \ $ lib "
     postdeps_CXX =

     ;;
  *Дарвин*)
     TARGET_OS = Darwin
     LEVELDB_TARGET_FLAGS = "- DOS_MACOSX"
     if test x $ cross_compiling! = xyes; тогда
       BUILD_OS = Darwin
       AC_PATH_PROGS ( [ RSVG_CONVERT ] , [ rsvg-convert rsvg ] , rsvg-convert )
       AC_CHECK_PROG ( [ BREW ] , варево , варево )
       if test x $ BREW = xbrew; тогда
         dnl Эти пакеты Homebrew могут быть только для бочонка, это означает, что они не будут найдены
         dnl в ожидаемых путях, потому что они могут конфликтовать с системными файлами. Спросить
         dnl Доморощенный, где каждый из них находится, затем отрегулируйте пути соответственно.
         dnl Безопасно добавлять эти пути, даже если функциональность отключена
         dnl пользователь (например, --without-wallet или --without-gui).

         bdb_prefix = $ ($ BREW --prefix berkeley-db4 2> / dev / null)
         qt5_prefix = $ ($ BREW --prefix qt5 2> / dev / null)
         if test x $ bdb_prefix! = x; тогда
           CPPFLAGS = "$ CPPFLAGS -I $ bdb_prefix / include"
           LIBS = "$ LIBS -L $ bdb_prefix / lib"
         фи
         if test x $ qt5_prefix! = x; тогда
           PKG_CONFIG_PATH = "$ qt5_prefix / Библиотека / pkg-config: $ PKG_CONFIG_PATH"
           экспортировать PKG_CONFIG_PATH
         фи
       фи
     еще
       case $ build_os в
         *Дарвин*)
           BUILD_OS = Darwin
           ;;
         *)
           AC_PATH_TOOL ( [ INSTALLNAMETOOL ] , [ install_name_tool ] , install_name_tool )
           AC_PATH_TOOL ( [ OTOOL ] , [ otool ] , otool )
           AC_PATH_PROGS ( [ GENISOIMAGE ] , [ genisoimage mkisofs ] , genisoimage )
           AC_PATH_PROGS ( [ RSVG_CONVERT ] , [ rsvg-convert rsvg ] , rsvg-convert )
           AC_PATH_PROGS ( [ IMAGEMAGICK_CONVERT ] , [ конвертировать ] , конвертировать )
           AC_PATH_PROGS ( [ TIFFCP ] , [ tiffcp ] , tiffcp )

           dnl libtool попытается удалить статический lib, что является проблемой для
           dnl перекрестно строит, потому что strip пытается вызвать жестко запрограммированный ld,
           DNL, которые могут не существовать в пути. Зачистка .a не
           DNL необходимо, так что просто отключите его.
           old_striplib =
           ;;
       ESAC
     фи

     AX_CHECK_LINK_FLAG ( [ [ -Wl, -headerpad_max_install_names ] ] , [ LDFLAGS = "$ LDFLAGS -Wl, -headerpad_max_install_names" ] )
     CPPFLAGS = "$ CPPFLAGS -DMAC_OSX -DOBJC_OLD_DISPATCH_PROTOTYPES = 0"
     OBJCXXFLAGS = "$ CXXFLAGS"
     ;;
   * Android *)
     dnl убедитесь, что android остается выше linux для таких хостов, как * linux-android *
     TARGET_OS = андроид
     LEVELDB_TARGET_FLAGS = "- DOS_ANDROID"
     ;;
   * Linux *)
     TARGET_OS = линукс
     LEVELDB_TARGET_FLAGS = "- DOS_LINUX"
     ;;
   * Kfreebsd *)
     LEVELDB_TARGET_FLAGS = "- DOS_KFREEBSD"
     ;;
   * * FreeBSD)
     LEVELDB_TARGET_FLAGS = "- DOS_FREEBSD"
     ;;
   * OpenBSD *)
     LEVELDB_TARGET_FLAGS = "- DOS_OPENBSD"
     ;;
   * NetBSD *)
     LEVELDB_TARGET_FLAGS = "- DOS_NETBSD"
     ;;
   * Стрекоза *)
     LEVELDB_TARGET_FLAGS = "- DOS_DRAGONFLYBSD"
     ;;
   * Солярис *)
     LEVELDB_TARGET_FLAGS = "- DOS_SOLARIS"
     ;;
   * HPUX *)
     LEVELDB_TARGET_FLAGS = "- DOS_HPUX"
     ;;
   *)
     AC_MSG_ERROR ( Не удается  построить  LevelDB  для  $ хоста.  Пожалуйста ,  файл  с  черепашкой  отчета. )
     ;;
ESAC

if test x $ use_pkgconfig = xyes; тогда
  m4_ifndef ( [ PKG_PROG_PKG_CONFIG ] , [ AC_MSG_ERROR ( макрос PKG_PROG_PKG_CONFIG  не найден. Пожалуйста, установите pkg-config и перезапустите autogen.sh. ) ]         )
  m4_ifdef ( [ PKG_PROG_PKG_CONFIG ] , [
  PKG_PROG_PKG_CONFIG
  if test x "$ PKG_CONFIG" = "x"; тогда
    AC_MSG_ERROR ( pkg-config  не  найден. )
  фи
  ] )
фи

if test x $ use_extended_functional_tests! = xno; тогда
  AC_SUBST ( EXTENDED_FUNCTIONAL_TESTS , - расширенный )
фи

if test x $ use_lcov = xyes; тогда
  if test x $ LCOV = x; тогда
    AC_MSG_ERROR ( "  тестирование  lcov запрошено,  но  lcov  не  найдено" )
  фи
  if test x $ GCOV = x; тогда
    AC_MSG_ERROR ( "  тестирование  lcov запрошено,  но  gcov  не  найдено" )
  фи
  if test x $ PYTHON = x; тогда
    AC_MSG_ERROR ( "  тестирование  lcov запрошено,  но  python  не  найден" )
  фи
  if test x $ GENHTML = x; тогда
    AC_MSG_ERROR ( "  тестирование  lcov запрошено,  но  genhtml  не  найден" )
  фи
  LCOV = "$ LCOV --gcov-tool = $ GCOV"
  AX_CHECK_LINK_FLAG ( [ [ --coverage ] ] , [ LDFLAGS = "$ LDFLAGS --coverage" ] ,
    [ AC_MSG_ERROR ( «lcov  тестирование  просил ,  но  - покрытие  компоновщик  флаг  делает  не  работу» ) ] )
  AX_CHECK_COMPILE_FLAG ( [ --coverage ] , [ CXXFLAGS = "$ CXXFLAGS --coverage" ] ,
    [ AC_MSG_ERROR ( «lcov  тестирование  просил ,  но  - покрытие  флаг  делает  не  работу» ) ] )
  AC_DEFINE ( USE_COVERAGE , 1 , [ Определить этот символ, если покрытие включено ] )
  CXXFLAGS = "$ CXXFLAGS -Og"
фи

if test x $ use_lcov_branch! = xno; тогда
  AC_SUBST ( LCOV_OPTS , "$ LCOV_OPTS  - rc  lcov_branch_coverage = 1" )
фи

dnl проверка на порядковый номер
AC_C_BIGENDIAN

dnl Проверить требования к компиляции / ссылке pthread
AX_PTHREAD

dnl Следующий макрос добавит необходимые определения в bitcoin-config.h, но
DnL они также должны быть переданы в любые подпроекты. Вытащить результаты из
Удалите кеш и добавьте их в CPPFLAGS.
AC_SYS_LARGEFILE
dnl обнаруживает POSIX или GNU вариант strerror_r
AC_FUNC_STRERROR_R

if test x $ ac_cv_sys_file_offset_bits! = x &&
   test x $ ac_cv_sys_file_offset_bits! = xno &&
   test x $ ac_cv_sys_file_offset_bits! = xunknown; тогда
  CPPFLAGS = "$ CPPFLAGS -D_FILE_OFFSET_BITS = $ ac_cv_sys_file_offset_bits"
фи

if test x $ ac_cv_sys_large_files! = x &&
   test x $ ac_cv_sys_large_files! = xno &&
   test x $ ac_cv_sys_large_files! = xunknown; тогда
  CPPFLAGS = "$ CPPFLAGS -D_LARGE_FILES = $ ac_cv_sys_large_files"
фи

AX_CHECK_LINK_FLAG ( [ [ -Wl, - с поддержкой больших адресов ] ] , [ LDFLAGS = "$ LDFLAGS -Wl, - с учетом больших адресов" ] )

AX_GCC_FUNC_ATTRIBUTE ( [ видимость ] )
AX_GCC_FUNC_ATTRIBUTE ( [ dllexport ] )
AX_GCC_FUNC_ATTRIBUTE ( [ dllimport ] )

if test x $ use_glibc_compat! = xno; тогда

  Параметры и тип возвращаемого значения dnl __fdelt_chk изменились с long unsigned int на long int.
  dnl Посмотрите, кто здесь присутствует.
  AC_MSG_CHECKING ( тип __fdelt_chk  )
  AC_COMPILE_IFELSE ( [ AC_LANG_PROGRAM ( [ [ #ifdef _FORTIFY_SOURCE
                    #undef _FORTIFY_SOURCE
                  #endif
                  #define _FORTIFY_SOURCE 2
                  #include <sys / select.h>
     extern "C" long unsigned int __fdelt_warn (long unsigned int); ] ] , [ [ ] ] ) ] ,
    [ fdelt_type = "long unsigned int" ] ,
    [ fdelt_type = "long int" ] )
  AC_MSG_RESULT ( $ fdelt_type )
  AC_DEFINE_UNQUOTED ( FDELT_TYPE , $ fdelt_type , [ параметр и тип возвращаемого значения для __fdelt_chk ] )
  AX_CHECK_LINK_FLAG ( [ [ -Wl, - wrap = __ divmoddi4 ] ] , [ COMPAT_LDFLAGS = "$ COMPAT_LDFLAGS -Wl, - wrap = __ divmoddi4" ] )
  AX_CHECK_LINK_FLAG ( [ [ -Wl, - wrap = log2f ] ] , [ COMPAT_LDFLAGS = "$ COMPAT_LDFLAGS -Wl, - wrap = log2f" ] )
еще
  AC_SEARCH_LIBS ( [ clock_gettime ] , [ rt ] )
фи

if test "x $ enable_gprof" = xyes; тогда
    dnl -pg несовместим с -pie. Поскольку упрочнение и профилирование вместе не имеет смысла,
    DnL мы просто делаем их взаимоисключающими здесь. Кроме того, закаленные цепи могут вызвать
    По умолчанию dnl -pie, в этом случае его необходимо отключить с помощью -no-pie.

    if test x $ use_hardening = xyes; тогда
        AC_MSG_ERROR ( дргоЕ  профилирование  это  не  совместим  с  закалкой.  Перенастройка  с  - отключить-твердеющий  или  - отключить-дргиЙ )
    фи
    use_hardening = нет
    AX_CHECK_COMPILE_FLAG ( [ -pg ] , [ GPROF_CXXFLAGS = "- pg" ] ,
        [ AC_MSG_ERROR ( дргоЕ  профилирование  просил ,  но  не  доступен ) ] , [ [ $ CXXFLAG_WERROR ] ] )

    AX_CHECK_LINK_FLAG ( [ [ -no-pie ] ] , [ GPROF_LDFLAGS = "- no-pie" ] )
    AX_CHECK_LINK_FLAG ( [ [ -pg ] ] , [ GPROF_LDFLAGS = "$ GPROF_LDFLAGS -pg" ] ,
        [ AC_MSG_ERROR ( дргоЕ  профилирование  просил ,  но  не  доступен ) ] , [ [ $ GPROF_LDFLAGS ] ] )
фи

if test x $ TARGET_OS! = xwindows; тогда
  dnl Весь код Windows - PIC, принудительное включение просто добавляет бесполезные предупреждения компиляции
  AX_CHECK_COMPILE_FLAG ( [ -fPIC ] , [ PIC_FLAGS = "- fPIC" ] )
фи

dnl Все версии gcc, которые мы обычно используем для сборки, подвержены ошибкам
dnl https://gcc.gnu.org/bugzilla/show_bug.cgi?id=90348. Чтобы обойти это, установите
dnl -fstack-reuse = none для всех сборок gcc. (Только gcc понимает этот флаг)
AX_CHECK_COMPILE_FLAG ( [ -fstack-reuse = none ] , [ HARDENED_CXXFLAGS = "$ HARDENED_CXXFLAGS -fstack-reuse = none" ] )
if test x $ use_hardening! = xno; тогда
  use_hardening = да
  AX_CHECK_COMPILE_FLAG ( [ -Wstack-protector ] , [ HARDENED_CXXFLAGS = "$ HARDENED_CXXFLAGS -Wstack-protector" ] )
  AX_CHECK_COMPILE_FLAG ( [ -fstack-protector-all ] , [ HARDENED_CXXFLAGS = "$ HARDENED_CXXFLAGS -fstack-protector-all" ] )

  dnl Когда enable_debug - yes, все оптимизации отключены.
  dnl Однако FORTIFY_SOURCE требует некоторого уровня оптимизации, в противном случае он ничего не делает и просто создает предупреждение компилятора.
  dnl Так как FORTIFY_SOURCE не может работать без оптимизации, не включайте его, если enable_debug имеет значение yes.
  if test x $ enable_debug! = xyes; тогда
    AX_CHECK_PREPROC_FLAG ( [ -D_FORTIFY_SOURCE = 2 ] , [
      AX_CHECK_PREPROC_FLAG ( [ -U_FORTIFY_SOURCE ] , [
        HARDENED_CPPFLAGS = "$ HARDENED_CPPFLAGS -U_FORTIFY_SOURCE"
      ] )
      HARDENED_CPPFLAGS = "$ HARDENED_CPPFLAGS -D_FORTIFY_SOURCE = 2"
    ] )
  фи

  AX_CHECK_LINK_FLAG ( [ [ -Wl, - dynamicbase ] ] , [ HARDENED_LDFLAGS = "$ HARDENED_LDFLAGS -Wl, - dynamicbase" ] )
  AX_CHECK_LINK_FLAG ( [ [ -Wl, - nxcompat ] ] , [ HARDENED_LDFLAGS = "$ HARDENED_LDFLAGS -Wl, - nxcompat" ] )
  AX_CHECK_LINK_FLAG ( [ [ -Wl, - high-entropy-va ] ] , [ HARDENED_LDFLAGS = "$ HARDENED_LDFLAGS -Wl, - high-entropy-va" ] )
  AX_CHECK_LINK_FLAG ( [ [ -Wl, -z, relro ] ] , [ HARDENED_LDFLAGS = "$ HARDENED_LDFLAGS -Wl, -z, relro" ] )
  AX_CHECK_LINK_FLAG ( [ [ -Wl, -z, сейчас ] ] , [ HARDENED_LDFLAGS = "$ HARDENED_LDFLAGS -Wl, -z, сейчас" ] )
  AX_CHECK_LINK_FLAG ( [ [ -fPIE -pie ] ] , [ PIE_FLAGS = "- fPIE"; HARDENED_LDFLAGS = "$ HARDENED_LDFLAGS -pie" ] ,, [ [ $ CXXFLAG_WERROR ] ] )

  case $ host in
    * MinGW *)
       AC_CHECK_LIB ( [ ssp ] ,       [ main ] ,, AC_MSG_ERROR ( отсутствует libssp  ) )
    ;;
  ESAC
фи

Этот флаг портит не-Дарвин GCC, даже если проверка не проходит. это особый случай.
if test x $ TARGET_OS = xdarwin; тогда
  AX_CHECK_LINK_FLAG ( [ [ -Wl, -dead_strip ] ] , [ LDFLAGS = "$ LDFLAGS -Wl, -dead_strip" ] )
  AX_CHECK_LINK_FLAG ( [ [ -Wl, -dead_strip_dylibs ] ] , [ LDFLAGS = "$ LDFLAGS -Wl, -dead_strip_dylibs" ] )
  AX_CHECK_LINK_FLAG ( [ [ -Wl, -bind_at_load ] ] , [ HARDENED_LDFLAGS = "$ HARDENED_LDFLAGS -Wl, -bind_at_load" ] )
фи

AC_CHECK_HEADERS ( [ endian.h sys / endian.h byteswap.h stdio.h stdlib.h unistd.h strings.h sys / types.h sys / stat.h sys / select.h sys / prctl.h sys / sysctl. h vm / vm_param.h sys / vmmeter.h sys / resources.h ] )

dnl FD_ZERO может зависеть от объявления memcpy, например, в SmartOS
dnl проверяет, что он не может быть собран без memcpy, а затем он собирается с
AC_MSG_CHECKING ( зависимость FD_ZERO  memcpy  )
AC_COMPILE_IFELSE ( [ AC_LANG_PROGRAM ( [ [
    #include <cstddef>
    #if HAVE_SYS_SELECT_H
    #include <sys / select.h>
    #endif
  ] ] , [ [
    #if HAVE_SYS_SELECT_H
    fd_set fds;
    FD_ZERO (& FDS);
    #endif
  ] ] )],
  [  AC_MSG_RESULT ( нет )  ] ,
  [
      AC_COMPILE_IFELSE ( [ AC_LANG_PROGRAM ( [ [
          #include <cstring>
          #if HAVE_SYS_SELECT_H
          #include <sys / select.h>
          #endif
        ] ] , [ [
          #if HAVE_SYS_SELECT_H
          fd_set fds;
          FD_ZERO (& FDS);
          #endif
        ] ] )],
        [  AC_MSG_RESULT ( да ) ; AC_DEFINE ( HAVE_CSTRING_DEPENDENT_FD_ZERO , 1 , [ Определите этот символ, если FD_ZERO зависит от наличия объявления memcpy ] )  ] ,
        [  AC_MSG_ERROR ( не удалось  с  CString  включают в себя )  ]
      )
  ]
)

AC_CHECK_DECLS ( [ getifaddrs, freeifaddrs ] ,,,
    [ #include <sys / types.h>
    #include <ifaddrs.h> ]
)
AC_CHECK_DECLS ( [ strnlen ] )

dnl Проверить наличие демона (3), не связанного с --with-daemon (хотя и используется им)
AC_CHECK_DECLS ( [ демон ] )

AC_CHECK_DECLS ( [ le16toh, le32toh, le64toh, htole16, htole32, htole64, be16toh, be32toh, be64toh, htobe16, htobe32, htobe64 ] ,,,
		[ #if HAVE_ENDIAN_H
                 #include <endian.h>
                 #elif HAVE_SYS_ENDIAN_H
                 #include <sys / endian.h>
                 #endif ] )

AC_CHECK_DECLS ( [ bswap_16, bswap_32, bswap_64 ] ,,,
		[ #if HAVE_BYTESWAP_H
                 #include <byteswap.h>
                 #endif ] )

AC_CHECK_DECLS ( [ __builtin_clz, __builtin_clzl, __builtin_clzll ] )

dnl Проверка для malloc_info (для информации о статистике памяти в getmemoryinfo)
AC_MSG_CHECKING ( для  getmemoryinfo )
AC_COMPILE_IFELSE ( [ AC_LANG_PROGRAM ( [ [ #include <malloc.h> ] ] ,
 [ [ INT F = malloc_info (0, NULL); ] ] ) ] ,
 [  AC_MSG_RESULT ( да ) ; AC_DEFINE ( HAVE_MALLOC_INFO , 1 , [ Определите этот символ, если у вас есть malloc_info ] )  ] ,
 [  AC_MSG_RESULT ( нет ) ]
)

dnl Проверка на наличие ошибок (M_ARENA_MAX) (для настройки glibc arenas)
AC_MSG_CHECKING ( для  неправильной  M_ARENA_MAX )
AC_COMPILE_IFELSE ( [ AC_LANG_PROGRAM ( [ [ #include <malloc.h> ] ] ,
 [ [ mallopt (M_ARENA_MAX, 1); ] ] ) ] ,
 [  AC_MSG_RESULT ( да ) ; AC_DEFINE ( HAVE_MALLOPT_ARENA_MAX , 1 , [ Определите этот символ, если у вас неправильный выбор с M_ARENA_MAX ] )  ] ,
 [  AC_MSG_RESULT ( нет ) ]
)

AC_MSG_CHECKING ( [ для атрибута видимости ] )
AC_LINK_IFELSE ( [ AC_LANG_SOURCE ( [
  int foo_def (void) __attribute __ ((visibility ("default")));
  int main () {}
  ] ) ] ,
  [
    AC_DEFINE ( HAVE_VISIBILITY_ATTRIBUTE , 1 , [ Определить, поддерживается ли атрибут видимости. ] )
    AC_MSG_RESULT ( да )
  ] ,
  [
    AC_MSG_RESULT ( нет )
    if test x $ use_reduce_exports = xyes; тогда
      AC_MSG_ERROR ( [ Не удается найти работающий атрибут видимости. Используйте --disable-redu-exports. ] )
    фи
  ]
)

if test "x $ use_thread_local" = xyes || {test "x $ use_thread_local" = xauto && test "x $ use_glibc_compat" = xno; }; тогда
  TEMP_LDFLAGS = "$ LDFLAGS"
  LDFLAGS = "$ TEMP_LDFLAGS $ PTHREAD_CFLAGS"
  AC_MSG_CHECKING ( [ для поддержки thread_local ] )
  AC_LINK_IFELSE ( [ AC_LANG_SOURCE ( [
    #include <thread>
    static thread_local int foo = 0;
    static void run_thread () {foo ++;}
    int main () {
    for (int i = 0; i <10; i ++) {std :: thread (run_thread) .detach ();}
    вернуть foo;
    }
    ] ) ] ,
    [
     case $ host in
       * MinGW *)
          Реализация thread_local в dnl mingw32 также показала себя
          dnl ошибочно при одновременном использовании; видеть:
          dnl https://gist.github.com/jamesob/fe9a872051a88b2025b1aa37bfa98605
          AC_MSG_RESULT ( нет )
          ;;
        *Дарвин*)
          dnl TODO включает thread_local в более поздних версиях Darwin, где он
          dnl поддерживается (для https://stackoverflow.com/a/29929949)
          AC_MSG_RESULT ( нет )
          ;;
        * * FreeBSD)
          Реализация thread_local во FreeBSD также содержит ошибки
          dnl https://groups.google.com/d/msg/bsdmailinglist/22ncTZAbDp4/Dii_pII5AwAJ)
          AC_MSG_RESULT ( нет )
          ;;
        *)
          AC_DEFINE ( HAVE_THREAD_LOCAL , 1 , [ определить, поддерживается ли thread_local. ] )
          AC_MSG_RESULT ( да )
          ;;
      ESAC
    ] ,
    [
      AC_MSG_RESULT ( нет )
    ]
  )
  LDFLAGS = "$ TEMP_LDFLAGS"
фи

dnl Проверка на разные способы сбора ОС случайности
AC_MSG_CHECKING ( для  системного вызова getrandom для Linux  ) 
AC_COMPILE_IFELSE ( [ AC_LANG_PROGRAM ( [ [ #include <unistd.h>
  #include <sys / syscall.h>
  #include <linux / random.h> ] ] ,
 [ [ syscall (SYS_getrandom, nullptr, 32, 0); ] ] ) ] ,
 [  AC_MSG_RESULT ( да ) ; AC_DEFINE ( HAVE_SYS_GETRANDOM , 1 , [ Определить этот символ, если доступен системный вызов getrandom в Linux ] )  ] ,
 [  AC_MSG_RESULT ( нет ) ]
)

AC_MSG_CHECKING ( для  геентропии )
AC_COMPILE_IFELSE ( [ AC_LANG_PROGRAM ( [ [ #include <unistd.h> ] ] ,
 [ [ getentropy (nullptr, 32) ] ] ) ] ,
 [  AC_MSG_RESULT ( да ) ; AC_DEFINE ( HAVE_GETENTROPY , 1 , [ Определить этот символ, если доступен системный вызов getentropy BSD ] )  ] ,
 [  AC_MSG_RESULT ( нет ) ]
)

AC_MSG_CHECKING ( для  геентропии  через  random.h )
AC_COMPILE_IFELSE ( [ AC_LANG_PROGRAM ( [ [ #include <unistd.h>
#include <sys / random.h> ] ] ,
 [ [ getentropy (nullptr, 32) ] ] ) ] ,
 [  AC_MSG_RESULT ( да ) ; AC_DEFINE ( HAVE_GETENTROPY_RAND , 1 , [ Определить этот символ, если системный вызов getentropy BSD доступен с sys / random.h ] )  ] ,
 [  AC_MSG_RESULT ( нет ) ]
)

AC_MSG_CHECKING ( для  sysctl )
AC_COMPILE_IFELSE ( [ AC_LANG_PROGRAM ( [ [ #include <sys / types.h>
  #include <sys / sysctl.h> ] ] ,
 [ [ static const int name [ 2 ] = {CTL_KERN, KERN_VERSION};
    #ifdef __linux__
    #error "Не используйте sysctl в Linux, он устарел, даже когда работает"
    #endif
    sysctl (name, 2, nullptr, nullptr, nullptr, 0); ] ] ) ] ,
 [  AC_MSG_RESULT ( да ) ; AC_DEFINE ( HAVE_SYSCTL , 1 , [ Определить этот символ, если BSD sysctl () доступен ] )  ] ,
 [  AC_MSG_RESULT ( нет ) ]
)

AC_MSG_CHECKING ( для  sysctl  KERN_ARND )
AC_COMPILE_IFELSE ( [ AC_LANG_PROGRAM ( [ [ #include <sys / types.h>
  #include <sys / sysctl.h> ] ] ,
 [ [ static const int name [ 2 ] = {CTL_KERN, KERN_ARND};
    sysctl (name, 2, nullptr, nullptr, nullptr, 0); ] ] ) ] ,
 [  AC_MSG_RESULT ( да ) ; AC_DEFINE ( HAVE_SYSCTL_ARND , 1 , [ Определить этот символ, если доступен BSD sysctl (KERN_ARND) ] )  ] ,
 [  AC_MSG_RESULT ( нет ) ]
)

AC_MSG_CHECKING ( для,  если  тип  char  равен  int8_t )
AC_COMPILE_IFELSE ( [ AC_LANG_PROGRAM ( [ [ #include <stdint.h>
  #include <type_traits> ] ] ,
 [ [ static_assert (std :: is_same <int8_t, char> :: value, ""); ] ] ) ] ,
 [  AC_MSG_RESULT ( да ) ; AC_DEFINE ( CHAR_EQUALS_INT8 , 1 , [ Определите этот символ, если тип char равен int8_t ] )  ] ,
 [  AC_MSG_RESULT ( нет ) ]
)

dnl Проверить на сокращение экспорта
if test x $ use_reduce_exports = xyes; тогда
  AX_CHECK_COMPILE_FLAG ( [ -fvisibility = скрыто ] , [ RE_CXXFLAGS = "- fvisibility = скрыто" ] ,
  [ AC_MSG_ERROR ( [ Невозможно установить видимость символа по умолчанию. Используйте --disable-redu-exports. ] ) ] )
фи

AC_MSG_CHECKING ( [ для std :: system ] )
AC_LINK_IFELSE (
    [  AC_LANG_PROGRAM (
        [ [ #include <cstdlib> ] ] ,
        [ [ int nErr = std :: system (""); ] ]
    ) ] ,
    [  AC_MSG_RESULT ( да ) ; AC_DEFINE ( HAVE_STD__SYSTEM , 1 , определение  в  1 ,  если  станд :: Система  является  доступна. ) ] ,
    [  AC_MSG_RESULT ( нет )  ]
)

AC_MSG_CHECKING ( [ для :: _системы ] )
AC_LINK_IFELSE (
    [  AC_LANG_PROGRAM (
        [ [  ] ] ,
        [ [ int nErr = :: _ wsystem (""); ] ]
    ) ] ,
    [  AC_MSG_RESULT ( да ) ; AC_DEFINE ( HAVE_WSYSTEM , 1 , определение  в  1 ,  если  :: wsystem  это  доступно. ) ] ,
    [  AC_MSG_RESULT ( нет )  ]
)

AC_DEFINE ( [ HAVE_SYSTEM ] , [ HAVE_STD__SYSTEM || HAVE_WSYSTEM ] , [ std :: system или :: wsystem ] )

LEVELDB_CPPFLAGS =
LIBLEVELDB =
LIBMEMENV =
AM_CONDITIONAL ( [ EMBEDDED_LEVELDB ] , [ верно ] )
AC_SUBST ( LEVELDB_CPPFLAGS )
AC_SUBST ( LIBLEVELDB )
AC_SUBST ( LIBMEMENV )

dnl enable-fuzz должен отключить все остальные цели
if test "x $ enable_fuzz" = "xyes"; тогда
  AC_MSG_WARN ( Enable-пух  будет  отключить  все  другие  цели )
  build_bitcoin_utils = нет
  build_bitcoin_cli = нет
  build_bitcoin_tx = нет
  build_bitcoin_wallet = нет
  build_bitcoind = нет
  build_bitcoin_libs = нет
  bitcoin_enable_qt = нет
  bitcoin_enable_qt_test = нет
  bitcoin_enable_qt_dbus = нет
  enable_wallet = нет
  use_bench = нет
  use_upnp = нет
  use_zmq = нет
еще
  BITCOIN_QT_INIT

  dnl устанавливает $ bitcoin_enable_qt, $ bitcoin_enable_qt_test, $ bitcoin_enable_qt_dbus
  BITCOIN_QT_CONFIGURE ( [ $ use_pkgconfig ] )
фи

if test x $ enable_wallet! = xno; тогда
    dnl Проверять libdb_cxx только если кошелек включен
    BITCOIN_FIND_BDB48
фи

dnl Проверить наличие libminiupnpc (необязательно)
if test x $ use_upnp! = xno; тогда
  AC_CHECK_HEADERS (
    [ miniupnpc / miniwget.h miniupnpc / miniupnpc.h miniupnpc / upnpcommands.h miniupnpc / upnperrors.h ] ,
    [ AC_CHECK_LIB ( [ miniupnpc ] , [ upnpDiscover ] , [ MINIUPNPC_LIBS = -lminiupnpc ] , [ have_miniupnpc = no ] ) ] ,
    [ have_miniupnpc = нет ]
  )
dnl Минимальная поддерживаемая версия API miniUPnPc установлена ​​на 10. Это сохраняет совместимость
dnl с пакетами Ubuntu 16.04 LTS и Debian 8 libminiupnpc-dev.
if test x $ have_miniupnpc! = xno; тогда
  AC_MSG_CHECKING ( [ поддерживается ли версия API miniUPnPc ] )
  AC_PREPROC_IFELSE ( [ AC_LANG_PROGRAM ( [ [
      @%: @ include <miniupnpc / miniupnpc.h>
    ] ] , [ [
      #if MINIUPNPC_API_VERSION> = 10
      // Все хорошо
      #else
      # ошибка Версия API miniUPnPc слишком старая
      #endif
    ] ] )],[
      AC_MSG_RESULT ( да )
    ] , [
    AC_MSG_RESULT ( нет )
    AC_MSG_WARN ( [ версия API miniUPnPc <10 не поддерживается, отключение поддержки UPnP. ] )
    have_miniupnpc = нет
  ] )
фи
фи

if test x $ build_bitcoin_wallet $ build_bitcoin_cli $ build_bitcoin_tx $ build_bitcoind $ bitcoin_enable_qt $ use_tests $ use_bench = xnonononononono; тогда
    use_boost = нет
еще
    use_boost = да
фи

if test x $ use_boost = xyes; тогда

dnl Минимально необходимая версия Boost
define ( MINIMUM_REQUIRED_BOOST , 1.47.0 )

dnl проверка на повышение бодрости
AX_BOOST_BASE ( [ MINIMUM_REQUIRED_BOOST ] )
if test x $ want_boost = xno; тогда
    AC_MSG_ERROR ( [ [ только libbitcoinconsensus может быть построен без повышения ] ] )
фи
AX_BOOST_SYSTEM
AX_BOOST_FILESYSTEM
AX_BOOST_THREAD
AX_BOOST_CHRONO

dnl Повышение с 1.56 до 1.62 позволяет использовать std :: atomic вместо собственного атомарного
Реализация счетчиков dnl . В версии 1.63 и более поздних по умолчанию используется std :: atomic.
m4_pattern_allow ( DBOOST_AC_USE_STD_ATOMIC )  dnl, иначе он обрабатывается как макрос
BOOST_CPPFLAGS = "- DBOOST_SP_USE_STD_ATOMIC -DBOOST_AC_USE_STD_ATOMIC $ BOOST_CPPFLAGS"

if test x $ use_reduce_exports = xyes; тогда
  AC_MSG_CHECKING ( [ для повышения работоспособности уменьшен экспорт ] )
  TEMP_CPPFLAGS = "$ CPPFLAGS"
  CPPFLAGS = "$ BOOST_CPPFLAGS $ CPPFLAGS"
  AC_PREPROC_IFELSE ( [ AC_LANG_PROGRAM ( [ [
      @%: @ include <boost / version.hpp>
    ] ] , [ [
      #if BOOST_VERSION> = 104900
      // Все хорошо
      #else
      # ошибка Повышенная версия слишком старая
      #endif
    ] ] )],[
      AC_MSG_RESULT ( да )
    ] , [
    AC_MSG_ERROR ( [ Известно, что бустовые версии <1.49 ломаются при сокращении экспорта. Используйте --disable-redu-exports. ] )
  ] )
  CPPFLAGS = "$ TEMP_CPPFLAGS"
фи
фи

if test x $ use_reduce_exports = xyes; тогда
    CXXFLAGS = "$ CXXFLAGS $ RE_CXXFLAGS"
    AX_CHECK_LINK_FLAG ( [ [ -Wl, - exclude-libs, ALL ] ] , [ RELDFLAGS = "- Wl, - exclude-libs, ALL" ] )
фи

if test x $ use_tests = xyes; тогда

  if test x $ HEXDUMP = x; тогда
    AC_MSG_ERROR ( шестнадцатеричное  это  требуется  для  испытаний )
  фи


  if test x $ use_boost = xyes; тогда

  AX_BOOST_UNIT_TEST_FRAMEWORK

  dnl Определите, нужен ли -DBOOST_TEST_DYN_LINK
  AC_MSG_CHECKING ( [ для динамического связанного буст-теста ] )
  TEMP_LIBS = "$ LIBS"
  LIBS = "$ LIBS $ BOOST_LDFLAGS $ BOOST_UNIT_TEST_FRAMEWORK_LIB"
  TEMP_CPPFLAGS = "$ CPPFLAGS"
  CPPFLAGS = "$ CPPFLAGS $ BOOST_CPPFLAGS"
  AC_LINK_IFELSE ( [ AC_LANG_SOURCE ( [
       #define BOOST_TEST_DYN_LINK
       #define BOOST_TEST_MAIN
        #include <boost / test / unit_test.hpp>
       ] ) ] ,
    [ AC_MSG_RESULT ( да ) ]
    [ TESTDEFS = "$ TESTDEFS -DBOOST_TEST_DYN_LINK" ] ,
    [ AC_MSG_RESULT ( нет ) ] )
  LIBS = "$ TEMP_LIBS"
  CPPFLAGS = "$ TEMP_CPPFLAGS"

  фи
фи

if test x $ use_boost = xyes; тогда

BOOST_LIBS = "$ BOOST_LDFLAGS $ BOOST_SYSTEM_LIB $ BOOST_FILESYSTEM_LIB $ BOOST_THREAD_LIB $ BOOST_CHRONO_LIB"


dnl Если boost (до 1.57) был собран без c ++ 11, он эмулировал перечисления
DNL с использованием конструкций C ++ 98. К сожалению, эта деталь реализации просочилась в
днл аби. Это было исправлено в 1.57.

dnl При сборке с установленной версией с использованием c ++ 11 заголовки выбираются
dnl на нативной поддержке enum в c ++ 11 и включите ее, однако она не сможет
днл ссылка. Это можно обойти, отключив c ++ 11 enoped enums, если линковка будет
DNL провал.
dnl BOOST_NO_SCOPED_ENUMS был изменен на BOOST_NO_CXX11_SCOPED_ENUMS в 1.51.

TEMP_LIBS = "$ LIBS"
LIBS = "$ BOOST_LIBS $ LIBS"
TEMP_CPPFLAGS = "$ CPPFLAGS"
CPPFLAGS = "$ CPPFLAGS $ BOOST_CPPFLAGS"
AC_MSG_CHECKING ( [ для несоответствующих расширений c ++ 11 с областями применения ] )
AC_LINK_IFELSE ( [ AC_LANG_PROGRAM ( [ [
  #include <boost / config.hpp>
  #include <boost / version.hpp>
  #if! определенные (BOOST_NO_SCOPED_ENUMS) &&! определенные (BOOST_NO_CXX11_SCOPED_ENUMS) && BOOST_VERSION <105700
  #define BOOST_NO_SCOPED_ENUMS
  #define BOOST_NO_CXX11_SCOPED_ENUMS
  #define CHECK
  #endif
  #include <boost / filesystem.hpp>
  ] ] , [ [
  # определено (ПРОВЕРИТЬ)
    boost :: filesystem :: copy_file ("foo", "bar");
  #else
    удушение;
  #endif
  ] ] )],
  [ AC_MSG_RESULT (не соответствует ) ; BOOST_CPPFLAGS = "$ BOOST_CPPFLAGS -DBOOST_NO_SCOPED_ENUMS -DBOOST_NO_CXX11_SCOPED_ENUMS" ] , [ AC_MSG_RESULT ( ok ) ] )
LIBS = "$ TEMP_LIBS"
CPPFLAGS = "$ TEMP_CPPFLAGS"

dnl Boost> = 1.50 использует sleep_for вместо устаревшего сна, однако
dnl был сломан с 1.50 до 1.52 при поддержке наносна. Используйте sleep_for, если
dnl рабочая версия доступна, иначе засыпаю . сон был удален
dnl после 1.56.
dnl Если ни один не доступен, прервать.
TEMP_LIBS = "$ LIBS"
LIBS = "$ BOOST_LIBS $ LIBS"
TEMP_CPPFLAGS = "$ CPPFLAGS"
CPPFLAGS = "$ CPPFLAGS $ BOOST_CPPFLAGS"
AC_LINK_IFELSE ( [ AC_LANG_PROGRAM ( [ [
  #include <boost / thread / thread.hpp>
  #include <boost / version.hpp>
  ] ] , [ [
  #if BOOST_VERSION> = 105000 && (! определенный (BOOST_HAS_NANOSLEEP) || BOOST_VERSION> = 105200)
      повышение :: this_thread :: sleep_for (повышение :: хроно :: миллисекунды (0));
  #else
   душить меня
  #endif
  ] ] )],
  [ boost_sleep = да;
     AC_DEFINE ( HAVE_WORKING_BOOST_SLEEP_FOR , 1 , [ Определить этот символ, если Boost sleep_for работает ] ) ] ,
  [ boost_sleep = нет ] )
LIBS = "$ TEMP_LIBS"
CPPFLAGS = "$ TEMP_CPPFLAGS"

if test x $ boost_sleep! = xyes; тогда
TEMP_LIBS = "$ LIBS"
LIBS = "$ BOOST_LIBS $ LIBS"
TEMP_CPPFLAGS = "$ CPPFLAGS"
CPPFLAGS = "$ CPPFLAGS $ BOOST_CPPFLAGS"
AC_LINK_IFELSE ( [ AC_LANG_PROGRAM ( [ [
  #include <boost / version.hpp>
  #include <boost / thread.hpp>
  #include <boost / date_time / posix_time / posix_time_types.hpp>
  ] ] , [ [
  #if BOOST_VERSION <= 105600
      повышение :: this_thread :: сна (повышение :: posix_time :: миллисекунды (0));
  #else
   душить меня
  #endif
  ] ] )],
  [ boost_sleep = да; AC_DEFINE ( HAVE_WORKING_BOOST_SLEEP , 1 , [ Определить этот символ, если улучшенный сон работает ] ) ] ,
  [ boost_sleep = нет ] )
LIBS = "$ TEMP_LIBS"
CPPFLAGS = "$ TEMP_CPPFLAGS"
фи

if test x $ boost_sleep! = xyes; тогда
  AC_MSG_ERROR ( Нет  работая  повышение  сна  реализации  не найдено. )
фи

фи

if test x $ use_pkgconfig = xyes; тогда
  : dnl
  m4_ifdef (
    [ PKG_CHECK_MODULES ] ,
    [
      if test x $ use_qr! = xno; тогда
        BITCOIN_QT_CHECK ( [ PKG_CHECK_MODULES ( [ QR ] , [ libqrencode ] , [ have_qrencode = yes ] , [ have_qrencode = no ] ) ] )
      фи
      if test x $ build_bitcoin_cli $ build_bitcoind $ bitcoin_enable_qt $ use_tests! = xnononono; тогда
        PKG_CHECK_MODULES ( [ EVENT ] , [ libevent ] ,, [ AC_MSG_ERROR ( libevent  не  найден. ) ] )
        if test x $ TARGET_OS! = xwindows; тогда
          PKG_CHECK_MODULES ( [ EVENT_PTHREADS ] , [ libevent_pthreads ] ,, [ AC_MSG_ERROR ( libevent_pthreads  не  найден. ) ] )
        фи
      фи
      if test "x $ use_zmq" = "xyes"; тогда
        PKG_CHECK_MODULES ( [ ZMQ ] , [ libzmq> = 4 ] ,
          [ AC_DEFINE ( [ ENABLE_ZMQ ] , [ 1 ] , [ Определение 1 , чтобы включить функции ZMQ ] ) ] ,
          [ AC_DEFINE ( [ ENABLE_ZMQ ] , [ 0 ] , [ Определить до 1, чтобы включить функции ZMQ ] )
           AC_MSG_WARN ( [ libzmq версии 4.x или выше не найден, отключение ] )
           use_zmq = нет ] )
      еще
          AC_DEFINE_UNQUOTED ( [ ENABLE_ZMQ ] , [ 0 ] , [ Определить до 1, чтобы включить функции ZMQ ] )
      фи
    ]
  )
еще

  if test x $ build_bitcoin_cli $ build_bitcoind $ bitcoin_enable_qt $ use_tests! = xnononono; тогда
    AC_CHECK_HEADER ( [ event2 / event.h ] ,, AC_MSG_ERROR ( Libevent  заголовки  отсутствуют ) , )
    AC_CHECK_LIB ( [ событие ] , [ основное ] , EVENT_LIBS = -levent , AC_MSG_ERROR ( освобождение  отсутствует ) )
    if test x $ TARGET_OS! = xwindows; тогда
      AC_CHECK_LIB ( [ event_pthreads ] , [ main ] , EVENT_PTHREADS_LIBS = -levent_pthreads , AC_MSG_ERROR ( libevent_pthreads  отсутствует ) )
    фи
  фи

  if test "x $ use_zmq" = "xyes"; тогда
     AC_CHECK_HEADER ( [ zmq.h ] ,
       [ AC_DEFINE ( [ ENABLE_ZMQ ] , [ 1 ] , [ Определение 1 , чтобы включить функции ZMQ ] ) ] ,
       [ AC_MSG_WARN ( [ zmq.h не найден, отключение поддержки zmq ] )
        use_zmq = нет
        AC_DEFINE ( [ ENABLE_ZMQ ] , [ 0 ] , [ Определить до 1, чтобы включить функции ZMQ ] ) ] )
     AC_CHECK_LIB ( [ zmq ] , [ zmq_ctx_shutdown ] , ZMQ_LIBS = -lzmq ,
       [ AC_MSG_WARN ( [ libzmq> = 4.0 не найден, отключение поддержки zmq ] )
        use_zmq = нет
        AC_DEFINE ( [ ENABLE_ZMQ ] , [ 0 ] , [ Определить до 1, чтобы включить функции ZMQ ] ) ] )
  еще
    AC_DEFINE_UNQUOTED ( [ ENABLE_ZMQ ] , [ 0 ] , [ Определить до 1, чтобы включить функции ZMQ ] )
  фи

  if test "x $ use_zmq" = "xyes"; тогда
    DnL Предположим libzmq был построен для статического связывания
    case $ host in
      * MinGW *)
        ZMQ_CFLAGS = "$ ZMQ_CFLAGS -DZMQ_STATIC"
      ;;
    ESAC
  фи

  if test x $ use_qr! = xno; тогда
    BITCOIN_QT_CHECK ( [ AC_CHECK_LIB ( [ qrencode ] , [ main ] , [ QR_LIBS = -lqrencode ] , [ have_qrencode = no ] ) ] )
    BITCOIN_QT_CHECK ( [ AC_CHECK_HEADER ( [ qrencode.h ] ,, have_qrencode = no ) ] )
  фи
фи

dnl RapidCheck тестирование на основе свойств

enable_property_tests = нет
if test "x $ use_rapidcheck" = xauto; тогда
    AC_CHECK_HEADERS ( [ rapidcheck.h ] , [ enable_property_tests = yes ] )
elif test "x $ use_rapidcheck"! = xno; тогда
    enable_property_tests = да
фи

RAPIDCHECK_LIBS =
if test "x $ enable_property_tests" = xyes; тогда
   RAPIDCHECK_LIBS = -lrapidcheck
фи
AC_SUBST ( RAPIDCHECK_LIBS )
AM_CONDITIONAL ( [ ENABLE_PROPERTY_TESTS ] , [ test x $ enable_property_tests = xyes ] )

dnl однозначная проверка

need_bundled_univalue = да

if test x $ build_bitcoin_wallet $ build_bitcoin_cli $ build_bitcoin_tx $ build_bitcoind $ bitcoin_enable_qt $ use_tests $ use_bench = xnonononononono; тогда
  need_bundled_univalue = нет
еще

if test x $ system_univalue! = xno; тогда
  found_univalue = нет
  if test x $ use_pkgconfig = xyes; тогда
    : # NOP
    m4_ifdef (
      [ PKG_CHECK_MODULES ] ,
      [
        PKG_CHECK_MODULES ( [ UNIVALUE ] , [ libunivalue> = 1.0.4 ] , [ found_univalue = yes ] , [ true ] )
      ]
    )
  еще
    AC_CHECK_HEADER ( [ univalue.h ] , [
      AC_CHECK_LIB ( [ однозначный ] ,   [ основной ] , [
        UNIVALUE_LIBS = -lunivalue
        found_univalue = да
      ] , [ правда ] )
    ] , [ правда ] )
  фи

  if test x $ found_univalue = xyes; тогда
    system_univalue = да
    need_bundled_univalue = нет
  elif test x $ system_univalue = xyes; тогда
    AC_MSG_ERROR ( [ однозначный номер не найден ] )
  еще
    system_univalue = нет
  фи
фи

if test x $ need_bundled_univalue = xyes; тогда
  UNIVALUE_CFLAGS = '- I $ (SRCDIR) / univalue / включают'
  UNIVALUE_LIBS = 'univalue / libunivalue.la'
фи

фи

AM_CONDITIONAL ( [ EMBEDDED_UNIVALUE ] , [ Тест х $ need_bundled_univalue = xyes ] )
AC_SUBST ( UNIVALUE_CFLAGS )
AC_SUBST ( UNIVALUE_LIBS )

AC_MSG_CHECKING ( [ строить ли биткойн ] )
AM_CONDITIONAL ( [ BUILD_BITCOIND ] , [ test x $ build_bitcoind = xyes ] )
AC_MSG_RESULT ( $ build_bitcoind )

AC_MSG_CHECKING ( [ ли строить Bitcoin-кли ] )
AM_CONDITIONAL ( [ BUILD_BITCOIN_CLI ] , [ test x $ build_bitcoin_cli = xyes ] )
AC_MSG_RESULT ( $ build_bitcoin_cli )

AC_MSG_CHECKING ( [ собирать ли биткойн-tx ] )
AM_CONDITIONAL ( [ BUILD_BITCOIN_TX ] , [ test x $ build_bitcoin_tx = xyes ] )
AC_MSG_RESULT ( $ build_bitcoin_tx )

AC_MSG_CHECKING ( [ строить ли биткойн-кошелек ] )
AM_CONDITIONAL ( [ BUILD_BITCOIN_WALLET ] , [ test x $ build_bitcoin_wallet = xyes ] )
AC_MSG_RESULT ( $ build_bitcoin_wallet )

AC_MSG_CHECKING ( [ собирать ли библиотеки ] )
AM_CONDITIONAL ( [ BUILD_BITCOIN_LIBS ] , [ test x $ build_bitcoin_libs = xyes ] )
if test x $ build_bitcoin_libs = xyes; тогда
  AC_DEFINE ( HAVE_CONSENSUS_LIB , 1 , [ определить этот символ, если была достигнута согласованная библиотека ] )
  AC_CONFIG_FILES ( [ libbitcoinconsensus.pc: libbitcoinconsensus.pc.in ] )
фи
AC_MSG_RESULT ( $ build_bitcoin_libs )

AC_LANG_POP

if test "x $ use_ccache"! = "xno"; тогда
  AC_MSG_CHECKING ( если  CCache  должен  быть  использован )
  если тест х $ CCACHE = х; тогда
    if test "x $ use_ccache" = "xyes"; тогда
      AC_MSG_ERROR ( [ ccache not found. ] ) ;
    еще
      use_ccache = нет
    фи
  еще
    use_ccache = да
    CC = "$ ac_cv_path_CCACHE $ CC"
    CXX = "$ ac_cv_path_CCACHE $ CXX"
  фи
  AC_MSG_RESULT ( $ use_ccache )
фи
if test "x $ use_ccache" = "xyes"; тогда
    AX_CHECK_PREPROC_FLAG ( [ -Qunused-arguments ] , [ CPPFLAGS = "- Qunused-arguments $ CPPFLAGS" ] )
фи

DNL включить кошелек
AC_MSG_CHECKING ( [ если кошелек должен быть включен ] )
if test x $ enable_wallet! = xno; тогда
  AC_MSG_RESULT ( да )
  AC_DEFINE_UNQUOTED ( [ ENABLE_WALLET ] , [ 1 ] , [ Определить до 1 для включения функций кошелька ] )

еще
  AC_MSG_RESULT ( нет )
фи

dnl включить поддержку upnp
AC_MSG_CHECKING ( [ собирать ли с поддержкой UPnP ] )
if test x $ have_miniupnpc = xno; тогда
  if test x $ use_upnp = xyes; тогда
     AC_MSG_ERROR ( "UPnP  просил ,  но  не может  быть  построен.  Использование  - . Без-miniupnpc" )
  фи
  AC_MSG_RESULT ( нет )
  use_upnp = нет
еще
  if test x $ use_upnp! = xno; тогда
    AC_MSG_RESULT ( да )
    AC_MSG_CHECKING ( [ строить ли с включенной по умолчанию UPnP ] )
    use_upnp = да
    upnp_setting = 0
    if test x $ use_upnp_default! = xno; тогда
      use_upnp_default = да
      = 1 upnp_setting
    фи
    AC_MSG_RESULT ( $ use_upnp_default )
    AC_DEFINE_UNQUOTED ( [ USE_UPNP ] , [ $ upnp_setting ] , [ поддержка UPnP не компилируется, если она не определена, в противном случае значение (0 или 1) определяет состояние по умолчанию ] )
    if test x $ TARGET_OS = xwindows; тогда
      MINIUPNPC_CPPFLAGS = "- DSTATICLIB -DMINIUPNP_STATICLIB"
    фи
  еще
    AC_MSG_RESULT ( нет )
  фи
фи

dnl они используются только когда включен qt
BUILD_TEST_QT = ""
if test x $ bitcoin_enable_qt! = xno; тогда
  dnl включить поддержку dbus
  AC_MSG_CHECKING ( [ собирать ли графический интерфейс с поддержкой D-Bus ] )
  if test x $ bitcoin_enable_qt_dbus! = xno; тогда
    AC_DEFINE ( [ USE_DBUS ] , [ 1 ] , [ Определить, должна ли компилироваться поддержка dbus ] )
  фи
  AC_MSG_RESULT ( $ bitcoin_enable_qt_dbus )

  dnl включить поддержку qr
  AC_MSG_CHECKING ( [ собирать ли графический интерфейс с поддержкой QR-кодов ] )
  if test x $ have_qrencode = xno; тогда
    if test x $ use_qr = xyes; тогда
      AC_MSG_ERROR ( [ Поддержка QR запрошена, но не может быть построена. Используйте --without-qrencode ] )
    фи
    use_qr = нет
  еще
    if test x $ use_qr! = xno; тогда
      AC_DEFINE ( [ USE_QRCODE ] , [ 1 ] , [ Определите, должна ли быть скомпилирована поддержка QR ] )
      use_qr = да
    фи
  фи
  AC_MSG_RESULT ( [ $ use_qr ] )

  if test x $ XGETTEXT = x; тогда
    AC_MSG_WARN ( « зная искомых  это  требуется  для  обновления  кварты  переводов» )
  фи

  AC_MSG_CHECKING ( [ собирать ли test_bitcoin-qt ] )
  if test x $ use_gui_tests $ bitcoin_enable_qt_test = xyesyes; тогда
    AC_MSG_RESULT ( [ да ] )
    BUILD_TEST_QT = "да"
  еще
    AC_MSG_RESULT ( [ нет ] )
  фи
фи

AM_CONDITIONAL ( [ ENABLE_ZMQ ] , [ test "x $ use_zmq" = "xyes" ] )

AC_MSG_CHECKING ( [ стоит ли строить test_bitcoin ] )
if test x $ use_tests = xyes; тогда
  AC_MSG_RESULT ( [ да ] )
  BUILD_TEST = "да"
еще
  AC_MSG_RESULT ( [ нет ] )
  BUILD_TEST = ""
фи

AC_MSG_CHECKING ( [ следует ли сократить экспорт ] )
if test x $ use_reduce_exports = xyes; тогда
  AC_MSG_RESULT ( [ да ] )
еще
  AC_MSG_RESULT ( [ нет ] )
фи

if test x $ build_bitcoin_wallet $ build_bitcoin_cli $ build_bitcoin_tx $ build_bitcoin_libs $ build_bitcoind $ bitcoin_enable_qt $ use_bench $ use_tests = xnononononononono; тогда
  AC_MSG_ERROR ( [ Нет целей! Пожалуйста, укажите хотя бы одно из: --with-utils --with-libs --with-daemon --with-gui --enable-bench или --enable-tests ] )
фи

AM_CONDITIONAL ( [ TARGET_DARWIN ] , [ test x $ TARGET_OS = xdarwin ] )
AM_CONDITIONAL ( [ BUILD_DARWIN ] , [ test x $ BUILD_OS = xdarwin ] )
AM_CONDITIONAL ( [ TARGET_WINDOWS ] , [ test x $ TARGET_OS = xwindows ] )
AM_CONDITIONAL ( [ ENABLE_WALLET ] , [ test x $ enable_wallet = xyes ] )
AM_CONDITIONAL ( [ ENABLE_TESTS ] , [ test x $ BUILD_TEST = xyes ] )
AM_CONDITIONAL ( [ ENABLE_FUZZ ] , [ test x $ enable_fuzz = xyes ] )
AM_CONDITIONAL ( [ ENABLE_QT ] , [ test x $ bitcoin_enable_qt = xyes ] )
AM_CONDITIONAL ( [ ENABLE_QT_TESTS ] , [ test x $ BUILD_TEST_QT = xyes ] )
AM_CONDITIONAL ( [ ENABLE_BENCH ] , [ test x $ use_bench = xyes ] )
AM_CONDITIONAL ( [ USE_QRCODE ] , [ test x $ use_qr = xyes ] )
AM_CONDITIONAL ( [ USE_LCOV ] , [ test x $ use_lcov = xyes ] )
AM_CONDITIONAL ( [ GLIBC_BACK_COMPAT ] , [ test x $ use_glibc_compat = xyes ] )
AM_CONDITIONAL ( [ HARDEN ] , [ Тест х $ use_hardening = xyes ] )
AM_CONDITIONAL ( [ ENABLE_HWCRC32 ] , [ test x $ enable_hwcrc32 = xyes ] )
AM_CONDITIONAL ( [ ENABLE_SSE41 ] , [ test x $ enable_sse41 = xyes ] )
AM_CONDITIONAL ( [ ENABLE_AVX2 ] , [ test x $ enable_avx2 = xyes ] )
AM_CONDITIONAL ( [ ENABLE_SHANI ] , [ test x $ enable_shani = xyes ] )
AM_CONDITIONAL ( [ USE_ASM ] , [ test x $ use_asm = xyes ] )

AC_DEFINE ( CLIENT_VERSION_MAJOR , _CLIENT_VERSION_MAJOR , [ Основная версия ] )
AC_DEFINE ( CLIENT_VERSION_MINOR , _CLIENT_VERSION_MINOR , [ Малая версия ] )
AC_DEFINE ( CLIENT_VERSION_REVISION , _CLIENT_VERSION_REVISION , [ Build revision ] )
AC_DEFINE ( CLIENT_VERSION_BUILD , _CLIENT_VERSION_BUILD , [ Сборка версий ] )
AC_DEFINE ( CLIENT_VERSION_IS_RELEASE , _CLIENT_VERSION_IS_RELEASE , [ версия выпущена ] )
AC_DEFINE ( COPYRIGHT_YEAR , _COPYRIGHT_YEAR , [ Год авторского права ] )
AC_DEFINE ( COPYRIGHT_HOLDERS , "_COPYRIGHT_HOLDERS" , [ Правообладатель (и) перед заменой% s ] )
AC_DEFINE ( COPYRIGHT_HOLDERS_SUBSTITUTION , "_COPYRIGHT_HOLDERS_SUBSTITUTION" , [ Замена% s в строке правообладателей ] )
define ( _COPYRIGHT_HOLDERS_FINAL , [ patsubst (_COPYRIGHT_HOLDERS, [ % s ] , [ _COPYRIGHT_HOLDERS_SUBSTITUTION ] ) ] )
AC_DEFINE ( COPYRIGHT_HOLDERS_FINAL , "_COPYRIGHT_HOLDERS_FINAL" , [ Владелец авторского права (s) ] )
AC_SUBST ( CLIENT_VERSION_MAJOR , _CLIENT_VERSION_MAJOR )
AC_SUBST ( CLIENT_VERSION_MINOR , _CLIENT_VERSION_MINOR )
AC_SUBST ( CLIENT_VERSION_REVISION , _CLIENT_VERSION_REVISION )
AC_SUBST ( CLIENT_VERSION_BUILD , _CLIENT_VERSION_BUILD )
AC_SUBST ( CLIENT_VERSION_IS_RELEASE , _CLIENT_VERSION_IS_RELEASE )
AC_SUBST ( COPYRIGHT_YEAR , _COPYRIGHT_YEAR )
AC_SUBST ( COPYRIGHT_HOLDERS , "_COPYRIGHT_HOLDERS" )
AC_SUBST ( COPYRIGHT_HOLDERS_SUBSTITUTION , "_COPYRIGHT_HOLDERS_SUBSTITUTION" )
AC_SUBST ( COPYRIGHT_HOLDERS_FINAL , "_COPYRIGHT_HOLDERS_FINAL" )
AC_SUBST ( BITCOIN_DAEMON_NAME )
AC_SUBST ( BITCOIN_GUI_NAME )
AC_SUBST ( BITCOIN_CLI_NAME )
AC_SUBST ( BITCOIN_TX_NAME )
AC_SUBST ( BITCOIN_WALLET_TOOL_NAME )

AC_SUBST ( RELDFLAGS )
AC_SUBST ( DEBUG_CPPFLAGS )
AC_SUBST ( WARN_CXXFLAGS )
AC_SUBST ( NOWARN_CXXFLAGS )
AC_SUBST ( DEBUG_CXXFLAGS )
AC_SUBST ( COMPAT_LDFLAGS )
AC_SUBST ( ERROR_CXXFLAGS )
AC_SUBST ( GPROF_CXXFLAGS )
AC_SUBST ( GPROF_LDFLAGS )
Макрос AC_SUBST ( HARDENED_CXXFLAGS )
Макрос AC_SUBST ( HARDENED_CPPFLAGS )
Макрос AC_SUBST ( HARDENED_LDFLAGS )
AC_SUBST ( PIC_FLAGS )
AC_SUBST ( PIE_FLAGS )
Макрос AC_SUBST ( SANITIZER_CXXFLAGS )
Макрос AC_SUBST ( SANITIZER_LDFLAGS )
AC_SUBST ( SSE42_CXXFLAGS )
AC_SUBST ( SSE41_CXXFLAGS )
AC_SUBST ( AVX2_CXXFLAGS )
AC_SUBST ( SHANI_CXXFLAGS )
AC_SUBST ( LIBTOOL_APP_LDFLAGS )
AC_SUBST ( USE_UPNP )
AC_SUBST ( USE_QRCODE )
AC_SUBST ( BOOST_LIBS )
AC_SUBST ( TESTDEFS )
AC_SUBST ( LEVELDB_TARGET_FLAGS )
AC_SUBST ( MINIUPNPC_CPPFLAGS )
AC_SUBST ( MINIUPNPC_LIBS )
AC_SUBST ( EVENT_LIBS )
AC_SUBST ( EVENT_PTHREADS_LIBS )
AC_SUBST ( ZMQ_LIBS )
AC_SUBST ( QR_LIBS )
AC_CONFIG_FILES ( [ Makefile src / Makefile doc / man / share для Makefile / setup.nsi share / qt / info.plist test / config.ini ] )
AC_CONFIG_FILES ( [ contrib / devtools / split-debug.sh ] , [ chmod + x contrib / devtools / split-debug.sh ] )
AM_COND_IF ( [ HAVE_DOXYGEN ] , [ AC_CONFIG_FILES ( [ doc / Doxyfile ] ) ] )
AC_CONFIG_LINKS ( [ contrib / filter-lcov.py: contrib / filter-lcov.py ] )
AC_CONFIG_LINKS ( [ тест / функционал / test_runner.py: тест / функционал / test_runner.py ] )
AC_CONFIG_LINKS ( [ test / util / bitcoin-util-test.py: test / util / bitcoin-util-test.py ] )
AC_CONFIG_LINKS ( [ test / util / rpcauth-test.py: test / util / rpcauth-test.py ] )

Проверки m4 dnl boost делают что-то действительно неприятное: они экспортируют эти переменные. Как
В результате они попадают в конфигурацию secp256k1, и происходят безумные вещи.
dnl Пока это не исправлено, и мы синхронизируемся, мы просто удалим их.
CPPFLAGS_TEMP = "$ CPPFLAGS"
сбросить CPPFLAGS
CPPFLAGS = "$ CPPFLAGS_TEMP"

LDFLAGS_TEMP = "$ LDFLAGS"
сбросить LDFLAGS
LDFLAGS = "$ LDFLAGS_TEMP"

LIBS_TEMP = "$ LIBS"
сбросить LIBS
LIBS = "$ LIBS_TEMP"

PKGCONFIG_PATH_TEMP = "$ PKG_CONFIG_PATH"
unset PKG_CONFIG_PATH
PKG_CONFIG_PATH = "$ PKGCONFIG_PATH_TEMP"

PKGCONFIG_LIBDIR_TEMP = "$ PKG_CONFIG_LIBDIR"
unset PKG_CONFIG_LIBDIR
PKG_CONFIG_LIBDIR = "$ PKGCONFIG_LIBDIR_TEMP"

if test x $ need_bundled_univalue = xyes; тогда
  AC_CONFIG_SUBDIRS ( [источник / однозначный номер ] )
фи

ac_configure_args = "$ {ac_configure_args} --disable-shared --with-pic --enable-benchmark = нет --with-bignum = нет --enable-module-recovery --disable-jni"
AC_CONFIG_SUBDIRS ( [ src / secp256k1 ] )

AC_OUTPUT

dnl Замените путь BUILDDIR на правильный путь Windows при компиляции в Native Windows
case $ {OS} в
   * Windows *)
     sed 's / BUILDDIR = "\ / \ ( [ [ az ] ] \) / BUILDDIR =" \ 1: /' test / config.ini> test / config-2.ini
     mv test / config-2.ini test / config.ini
   ;;
ESAC

эхо
echo "Параметры, используемые для компиляции и ссылки:"
echo "with wallet = $ enable_wallet"
echo "with gui / qt = $ bitcoin_enable_qt"
if test x $ bitcoin_enable_qt! = xno; тогда
    echo "with qr = $ use_qr"
фи
echo "with zmq = $ use_zmq"
echo "with test = $ use_tests"
if test x $ use_tests! = xno; тогда
    echo "with prop = $ enable_property_tests"
    echo "with fuzz = $ enable_fuzz"
фи
echo "with bench = $ use_bench"
echo "with upnp = $ use_upnp"
echo "use asm = $ use_asm"
echo "sanitizers = $ use_sanitizers"
echo "debug enabled = $ enable_debug"
echo "gprof enabled = $ enable_gprof"
echo "werror = $ enable_werror"
эхо
echo "target os = $ TARGET_OS"
echo "build os = $ BUILD_OS"
эхо
echo "CC = $ CC"
echo "CFLAGS = $ CFLAGS"
echo "CPPFLAGS = $ DEBUG_CPPFLAGS $ HARDENED_CPPFLAGS $ CPPFLAGS"
echo "CXX = $ CXX"
echo "CXXFLAGS = $ DEBUG_CXXFLAGS $ HARDENED_CXXFLAGS $ WARN_CXXFLAGS $ NOWARN_CXXFLAGS $ ERROR_CXXFLAGS $ GPROF_CXXFLAGS $ CXXFLAGS"
echo "LDFLAGS = $ PTHREAD_CFLAGS $ HARDENED_LDFLAGS $ GPROF_LDFLAGS $ LDFLAGS"
echo "ARFLAGS = $ ARFLAGS"
эхо
