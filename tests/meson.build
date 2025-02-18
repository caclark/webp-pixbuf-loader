fs = import('fs')

t1 = executable('t1', 't1.c', dependencies : [gdkpb, webp, webpdemux])
t2 = executable('t2', 't2.c', dependencies : [gdkpb, webp, webpdemux])
t3 = executable('t3', 't3.c', dependencies : [gdkpb, webp, webpdemux])
t4 = executable('t4', 't4.c', dependencies : [gdkpb, webp, webpdemux])
t_save       = executable('t_save',        't_save.c',       dependencies : [gdkpb, webp, webpdemux])
t_icc        = executable('t_icc',         't_icc.c',        dependencies : [gdkpb, webp, webpdemux, webpmux])
t_null_error = executable('t_null_error',  't_null_error.c', dependencies : [gdkpb, webp, webpdemux])
t_scaled     = executable('t_scaled',      't_scaled.c',     dependencies : [gdkpb, webp, webpdemux])
t_jpeg       = executable('t_jpeg',        't_jpeg.c',       dependencies : [gdkpb, webp, webpdemux])
t_large      = executable('t_large',       't_large.c',      dependencies : [gdkpb, webp, webpdemux, gio])

loaders_data = configuration_data()
loaders_data.set('MODULE_PATH', fs.as_posix(pbl_webp.full_path()))
loaders = configure_file(input: 'loaders.cache.in',
                         output : 'loaders.cache',
                         configuration : loaders_data)

test_env = ['GDK_PIXBUF_MODULE_FILE=' + meson.current_build_dir() / 'loaders.cache']
test_file_base = 'TEST_FILE=' + meson.current_source_dir() / 'data'

test('load 1x1 image',     t1, env : test_env + [ test_file_base / 't1.webp'])
test('load 200x200 image', t2, env : test_env + [ test_file_base / 't2.webp'])
test('load animation',     t3, env : test_env + [ test_file_base / 't3.webp'])
test('get file info',      t4, env : test_env + [ test_file_base / 't1.webp'])
test('save data',         t_save, env : test_env + [ test_file_base / 't2.webp'])
test('icc data',           t_icc, env : test_env + [ test_file_base / 't2.webp'])
test('NULL GError', t_null_error, env : test_env + [ test_file_base / 't2.webp'])
test('large file',       t_large, env : test_env + [ test_file_base / 't_large.webp'])
test('scaled image',    t_scaled, env : test_env + [ test_file_base / 't2.webp', 'TEST_FILE_ANIM=' + meson.current_source_dir() / 'data' / 't3.webp'])
test('jpeg with .webp extension', t_jpeg, env : test_env + [ test_file_base / 'test_jpeg_as_webp.webp'])