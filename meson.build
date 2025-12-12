project(
  'pyodbc',
  'cpp',
  version : '5.3.0',
)

python = import('python').find_installation()
python_dep = python.dependency()

compiler = meson.get_compiler('cpp')

# ODBC driver needs to be installed by the OS.
odbc_dep = compiler.find_library('odbc')

pyodbc_sources = [
  'src/cnxninfo.cpp',
  'src/connection.cpp',
  'src/cursor.cpp',
  'src/decimal.cpp',
  'src/errors.cpp',
  'src/getdata.cpp',
  'src/params.cpp',
  'src/pyodbcdbg.cpp',
  'src/pyodbcmodule.cpp',
  'src/row.cpp',
  'src/textenc.cpp',
]
pyodbc_inc = include_directories(
  'src',
  is_system: true
)

add_project_arguments(
  [
    '-DPYODBC_VERSION=' + meson.project_version(),
    '-Wno-write-strings',
    '-Wno-deprecated-declarations',
  ],
  language: 'cpp'
)

# Build the pyodbc module
python.extension_module(
  'pyodbc',
  pyodbc_sources,
  dependencies : [
    python_dep,
    odbc_dep,
  ],
  include_directories : [pyodbc_inc],
  install : true,
  cpp_args : run_command(['odbc_config', '--cflags'], check : true).stdout().strip(),
  link_args : run_command(['odbc_config', '--libs'], check : true).stdout().strip(),
)
