load('//:subdir_glob.bzl', 'subdir_glob')

genrule(
  name = 'cmake',
  out = 'out',
  srcs = glob([
    '*.ac',
    '*.txt',
    'cmake/**/*.cmake',
    'cmake/**/*.in',
    'lib/*.c',
    'lib/*.h',
    'lib/*.txt',
    'src/*.c',
    'src/*.h',
    'src/*.in',
    'src/*.txt',
  ]),
  cmd = ' && '.join([
    'mkdir -p $OUT',
    'cd $OUT',
    'cmake -DCHECK_ENABLE_TESTS=OFF $SRCDIR',
  ]),
)

genrule(
  name = 'config-h',
  out = 'config.h',
  cmd = 'cp $(location :cmake)/config.h $OUT',
)

genrule(
  name = 'check-h',
  out = 'check.h',
  cmd = 'cp $(location :cmake)/src/check.h $OUT',
)

genrule(
  name = 'check-stdint-h',
  out = 'check_stdint.h',
  cmd = 'cp $(location :cmake)/check_stdint.h $OUT',
)

cxx_library(
  name = 'check',
  header_namespace = '',
  exported_headers = {
    'check.h': ':check-h',
    'check_stdint.h': ':check-stdint-h',
  },
  headers = subdir_glob([
    ('src', '*.h'),
    ('lib', '*.h'),
  ]),
  srcs = glob([
    'src/*.c',
    'lib/*.c',
  ]),
  visibility = [
    'PUBLIC',
  ],
)
