CMAKE_MINIMUM_REQUIRED(VERSION 2.8)

project(db)

IF (${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
add_compile_options(-Wno-deprecated-declarations -Wno-inaccessible-base -Wno-unused-local-typedefs -Wno-logical-op-parentheses -Wno-shift-negative-value -Wno-array-bounds)
endif()

set(DB_SOURCES
${CMAKE_CURRENT_SOURCE_DIR}/src/mutex/mut_tas.c
${CMAKE_CURRENT_SOURCE_DIR}/src/btree/bt_compare.c
${CMAKE_CURRENT_SOURCE_DIR}/src/btree/bt_compress.c
${CMAKE_CURRENT_SOURCE_DIR}/src/btree/bt_conv.c
${CMAKE_CURRENT_SOURCE_DIR}/src/btree/bt_curadj.c
${CMAKE_CURRENT_SOURCE_DIR}/src/btree/bt_cursor.c
${CMAKE_CURRENT_SOURCE_DIR}/src/btree/bt_delete.c
${CMAKE_CURRENT_SOURCE_DIR}/src/btree/bt_method.c
${CMAKE_CURRENT_SOURCE_DIR}/src/btree/bt_open.c
${CMAKE_CURRENT_SOURCE_DIR}/src/btree/bt_put.c
${CMAKE_CURRENT_SOURCE_DIR}/src/btree/bt_rec.c
${CMAKE_CURRENT_SOURCE_DIR}/src/btree/bt_reclaim.c
${CMAKE_CURRENT_SOURCE_DIR}/src/btree/bt_recno.c
${CMAKE_CURRENT_SOURCE_DIR}/src/btree/bt_rsearch.c
${CMAKE_CURRENT_SOURCE_DIR}/src/btree/bt_search.c
${CMAKE_CURRENT_SOURCE_DIR}/src/btree/bt_split.c
${CMAKE_CURRENT_SOURCE_DIR}/src/btree/bt_stat.c
${CMAKE_CURRENT_SOURCE_DIR}/src/btree/bt_compact.c
${CMAKE_CURRENT_SOURCE_DIR}/src/btree/bt_upgrade.c
${CMAKE_CURRENT_SOURCE_DIR}/src/btree/btree_auto.c
${CMAKE_CURRENT_SOURCE_DIR}/src/hash/hash.c
${CMAKE_CURRENT_SOURCE_DIR}/src/hash/hash_auto.c
${CMAKE_CURRENT_SOURCE_DIR}/src/hash/hash_compact.c
${CMAKE_CURRENT_SOURCE_DIR}/src/hash/hash_conv.c
${CMAKE_CURRENT_SOURCE_DIR}/src/hash/hash_dup.c
${CMAKE_CURRENT_SOURCE_DIR}/src/hash/hash_meta.c
${CMAKE_CURRENT_SOURCE_DIR}/src/hash/hash_method.c
${CMAKE_CURRENT_SOURCE_DIR}/src/hash/hash_open.c
${CMAKE_CURRENT_SOURCE_DIR}/src/hash/hash_page.c
${CMAKE_CURRENT_SOURCE_DIR}/src/hash/hash_rec.c
${CMAKE_CURRENT_SOURCE_DIR}/src/hash/hash_reclaim.c
${CMAKE_CURRENT_SOURCE_DIR}/src/hash/hash_stat.c
${CMAKE_CURRENT_SOURCE_DIR}/src/hash/hash_upgrade.c
${CMAKE_CURRENT_SOURCE_DIR}/src/hash/hash_verify.c
${CMAKE_CURRENT_SOURCE_DIR}/src/heap/heap.c
${CMAKE_CURRENT_SOURCE_DIR}/src/heap/heap_auto.c
${CMAKE_CURRENT_SOURCE_DIR}/src/heap/heap_backup.c
${CMAKE_CURRENT_SOURCE_DIR}/src/heap/heap_conv.c
${CMAKE_CURRENT_SOURCE_DIR}/src/heap/heap_method.c
${CMAKE_CURRENT_SOURCE_DIR}/src/heap/heap_open.c
${CMAKE_CURRENT_SOURCE_DIR}/src/heap/heap_rec.c
${CMAKE_CURRENT_SOURCE_DIR}/src/heap/heap_reclaim.c
${CMAKE_CURRENT_SOURCE_DIR}/src/heap/heap_stat.c
${CMAKE_CURRENT_SOURCE_DIR}/src/heap/heap_upgrade.c
${CMAKE_CURRENT_SOURCE_DIR}/src/heap/heap_verify.c
${CMAKE_CURRENT_SOURCE_DIR}/src/qam/qam.c
${CMAKE_CURRENT_SOURCE_DIR}/src/qam/qam_auto.c
${CMAKE_CURRENT_SOURCE_DIR}/src/qam/qam_conv.c
${CMAKE_CURRENT_SOURCE_DIR}/src/qam/qam_files.c
${CMAKE_CURRENT_SOURCE_DIR}/src/qam/qam_method.c
${CMAKE_CURRENT_SOURCE_DIR}/src/qam/qam_open.c
${CMAKE_CURRENT_SOURCE_DIR}/src/qam/qam_rec.c
${CMAKE_CURRENT_SOURCE_DIR}/src/qam/qam_stat.c
${CMAKE_CURRENT_SOURCE_DIR}/src/qam/qam_upgrade.c
${CMAKE_CURRENT_SOURCE_DIR}/src/qam/qam_verify.c
${CMAKE_CURRENT_SOURCE_DIR}/src/rep/rep_automsg.c
${CMAKE_CURRENT_SOURCE_DIR}/src/rep/rep_backup.c
${CMAKE_CURRENT_SOURCE_DIR}/src/rep/rep_elect.c
${CMAKE_CURRENT_SOURCE_DIR}/src/rep/rep_lease.c
${CMAKE_CURRENT_SOURCE_DIR}/src/rep/rep_log.c
${CMAKE_CURRENT_SOURCE_DIR}/src/rep/rep_method.c
${CMAKE_CURRENT_SOURCE_DIR}/src/rep/rep_record.c
${CMAKE_CURRENT_SOURCE_DIR}/src/rep/rep_region.c
${CMAKE_CURRENT_SOURCE_DIR}/src/rep/rep_stat.c
${CMAKE_CURRENT_SOURCE_DIR}/src/rep/rep_util.c
${CMAKE_CURRENT_SOURCE_DIR}/src/rep/rep_verify.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_addrinfo.c
${CMAKE_CURRENT_SOURCE_DIR}/src/repmgr/repmgr_auto.c
${CMAKE_CURRENT_SOURCE_DIR}/src/repmgr/repmgr_automsg.c
${CMAKE_CURRENT_SOURCE_DIR}/src/repmgr/repmgr_elect.c
${CMAKE_CURRENT_SOURCE_DIR}/src/repmgr/repmgr_method.c
${CMAKE_CURRENT_SOURCE_DIR}/src/repmgr/repmgr_msg.c
${CMAKE_CURRENT_SOURCE_DIR}/src/repmgr/repmgr_net.c
${CMAKE_CURRENT_SOURCE_DIR}/src/repmgr/repmgr_posix.c
${CMAKE_CURRENT_SOURCE_DIR}/src/repmgr/repmgr_queue.c
${CMAKE_CURRENT_SOURCE_DIR}/src/repmgr/repmgr_rec.c
${CMAKE_CURRENT_SOURCE_DIR}/src/repmgr/repmgr_sel.c
${CMAKE_CURRENT_SOURCE_DIR}/src/repmgr/repmgr_stat.c
${CMAKE_CURRENT_SOURCE_DIR}/src/repmgr/repmgr_util.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_ovfl_vrfy.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_vrfy.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_vrfyutil.c
${CMAKE_CURRENT_SOURCE_DIR}/src/btree/bt_verify.c
${CMAKE_CURRENT_SOURCE_DIR}/src/log/log_verify.c
${CMAKE_CURRENT_SOURCE_DIR}/src/log/log_verify_util.c
${CMAKE_CURRENT_SOURCE_DIR}/src/log/log_verify_int.c
${CMAKE_CURRENT_SOURCE_DIR}/src/log/log_verify_auto.c
${CMAKE_CURRENT_SOURCE_DIR}/src/lock/lock.c
${CMAKE_CURRENT_SOURCE_DIR}/src/lock/lock_deadlock.c
${CMAKE_CURRENT_SOURCE_DIR}/src/lock/lock_failchk.c
${CMAKE_CURRENT_SOURCE_DIR}/src/lock/lock_id.c
${CMAKE_CURRENT_SOURCE_DIR}/src/lock/lock_list.c
${CMAKE_CURRENT_SOURCE_DIR}/src/lock/lock_method.c
${CMAKE_CURRENT_SOURCE_DIR}/src/lock/lock_region.c
${CMAKE_CURRENT_SOURCE_DIR}/src/lock/lock_stat.c
${CMAKE_CURRENT_SOURCE_DIR}/src/lock/lock_timer.c
${CMAKE_CURRENT_SOURCE_DIR}/src/lock/lock_util.c
${CMAKE_CURRENT_SOURCE_DIR}/src/mutex/mut_alloc.c
${CMAKE_CURRENT_SOURCE_DIR}/src/mutex/mut_failchk.c
${CMAKE_CURRENT_SOURCE_DIR}/src/mutex/mut_method.c
${CMAKE_CURRENT_SOURCE_DIR}/src/mutex/mut_region.c
${CMAKE_CURRENT_SOURCE_DIR}/src/mutex/mut_stat.c
${CMAKE_CURRENT_SOURCE_DIR}/src/common/crypto_stub.c
${CMAKE_CURRENT_SOURCE_DIR}/src/blob/blob_fileops.c
${CMAKE_CURRENT_SOURCE_DIR}/src/blob/blob_page.c
${CMAKE_CURRENT_SOURCE_DIR}/src/blob/blob_stream.c
${CMAKE_CURRENT_SOURCE_DIR}/src/blob/blob_util.c
${CMAKE_CURRENT_SOURCE_DIR}/src/common/clock.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/crdel_auto.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/crdel_rec.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_am.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_auto.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_backup.c
${CMAKE_CURRENT_SOURCE_DIR}/src/common/db_byteorder.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_cam.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_cds.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_compact.c
${CMAKE_CURRENT_SOURCE_DIR}/src/common/db_compint.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_conv.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_copy.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_dispatch.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_dup.c
${CMAKE_CURRENT_SOURCE_DIR}/src/common/db_err.c
${CMAKE_CURRENT_SOURCE_DIR}/src/common/db_getlong.c
${CMAKE_CURRENT_SOURCE_DIR}/src/common/db_idspace.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_iface.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_join.c
${CMAKE_CURRENT_SOURCE_DIR}/src/common/db_log2.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_meta.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_method.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_open.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_overflow.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_pr.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_rec.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_reclaim.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_remove.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_rename.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_ret.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_setid.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_setlsn.c
${CMAKE_CURRENT_SOURCE_DIR}/src/common/db_shash.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_sort_multiple.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_stati.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_truncate.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_upg.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/db_upg_opd.c
${CMAKE_CURRENT_SOURCE_DIR}/src/dbreg/dbreg.c
${CMAKE_CURRENT_SOURCE_DIR}/src/dbreg/dbreg_stat.c
${CMAKE_CURRENT_SOURCE_DIR}/src/dbreg/dbreg_auto.c
${CMAKE_CURRENT_SOURCE_DIR}/src/dbreg/dbreg_rec.c
${CMAKE_CURRENT_SOURCE_DIR}/src/dbreg/dbreg_util.c
${CMAKE_CURRENT_SOURCE_DIR}/src/common/dbt.c
${CMAKE_CURRENT_SOURCE_DIR}/src/env/env_alloc.c
${CMAKE_CURRENT_SOURCE_DIR}/src/env/env_config.c
${CMAKE_CURRENT_SOURCE_DIR}/src/env/env_backup.c
${CMAKE_CURRENT_SOURCE_DIR}/src/env/env_failchk.c
${CMAKE_CURRENT_SOURCE_DIR}/src/env/env_file.c
${CMAKE_CURRENT_SOURCE_DIR}/src/env/env_globals.c
${CMAKE_CURRENT_SOURCE_DIR}/src/env/env_open.c
${CMAKE_CURRENT_SOURCE_DIR}/src/env/env_method.c
${CMAKE_CURRENT_SOURCE_DIR}/src/env/env_name.c
${CMAKE_CURRENT_SOURCE_DIR}/src/env/env_recover.c
${CMAKE_CURRENT_SOURCE_DIR}/src/env/env_region.c
${CMAKE_CURRENT_SOURCE_DIR}/src/env/env_register.c
${CMAKE_CURRENT_SOURCE_DIR}/src/env/env_sig.c
${CMAKE_CURRENT_SOURCE_DIR}/src/env/env_stat.c
${CMAKE_CURRENT_SOURCE_DIR}/src/fileops/fileops_auto.c
${CMAKE_CURRENT_SOURCE_DIR}/src/fileops/fop_basic.c
${CMAKE_CURRENT_SOURCE_DIR}/src/fileops/fop_rec.c
${CMAKE_CURRENT_SOURCE_DIR}/src/fileops/fop_util.c
${CMAKE_CURRENT_SOURCE_DIR}/src/hash/hash_func.c
${CMAKE_CURRENT_SOURCE_DIR}/src/hmac/hmac.c
${CMAKE_CURRENT_SOURCE_DIR}/src/log/log.c
${CMAKE_CURRENT_SOURCE_DIR}/src/log/log_archive.c
${CMAKE_CURRENT_SOURCE_DIR}/src/log/log_compare.c
${CMAKE_CURRENT_SOURCE_DIR}/src/log/log_debug.c
${CMAKE_CURRENT_SOURCE_DIR}/src/log/log_get.c
${CMAKE_CURRENT_SOURCE_DIR}/src/log/log_method.c
${CMAKE_CURRENT_SOURCE_DIR}/src/log/log_print.c
${CMAKE_CURRENT_SOURCE_DIR}/src/log/log_put.c
${CMAKE_CURRENT_SOURCE_DIR}/src/log/log_stat.c
${CMAKE_CURRENT_SOURCE_DIR}/src/common/mkpath.c
${CMAKE_CURRENT_SOURCE_DIR}/src/mp/mp_alloc.c
${CMAKE_CURRENT_SOURCE_DIR}/src/mp/mp_backup.c
${CMAKE_CURRENT_SOURCE_DIR}/src/mp/mp_bh.c
${CMAKE_CURRENT_SOURCE_DIR}/src/mp/mp_fget.c
${CMAKE_CURRENT_SOURCE_DIR}/src/mp/mp_fmethod.c
${CMAKE_CURRENT_SOURCE_DIR}/src/mp/mp_fopen.c
${CMAKE_CURRENT_SOURCE_DIR}/src/mp/mp_fput.c
${CMAKE_CURRENT_SOURCE_DIR}/src/mp/mp_fset.c
${CMAKE_CURRENT_SOURCE_DIR}/src/mp/mp_method.c
${CMAKE_CURRENT_SOURCE_DIR}/src/mp/mp_mvcc.c
${CMAKE_CURRENT_SOURCE_DIR}/src/mp/mp_region.c
${CMAKE_CURRENT_SOURCE_DIR}/src/mp/mp_register.c
${CMAKE_CURRENT_SOURCE_DIR}/src/mp/mp_resize.c
${CMAKE_CURRENT_SOURCE_DIR}/src/mp/mp_stat.c
${CMAKE_CURRENT_SOURCE_DIR}/src/mp/mp_sync.c
${CMAKE_CURRENT_SOURCE_DIR}/src/mp/mp_trickle.c
${CMAKE_CURRENT_SOURCE_DIR}/src/common/openflags.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_abort.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_abs.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_alloc.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_clock.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_cpu.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_ctime.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_config.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_dir.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_errno.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_fid.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_flock.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_fsync.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_getenv.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_handle.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_map.c
${CMAKE_CURRENT_SOURCE_DIR}/src/common/os_method.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_mkdir.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_open.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_path.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_pid.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_rename.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_rmdir.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_root.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_rpath.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_rw.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_seek.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_stack.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_stat.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_tmpdir.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_truncate.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_uid.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_unlink.c
${CMAKE_CURRENT_SOURCE_DIR}/src/os/os_yield.c
${CMAKE_CURRENT_SOURCE_DIR}/src/db/partition.c
${CMAKE_CURRENT_SOURCE_DIR}/src/sequence/seq_stat.c
${CMAKE_CURRENT_SOURCE_DIR}/src/sequence/sequence.c
${CMAKE_CURRENT_SOURCE_DIR}/src/hmac/sha1.c
${CMAKE_CURRENT_SOURCE_DIR}/src/clib/snprintf.c
${CMAKE_CURRENT_SOURCE_DIR}/src/txn/txn.c
${CMAKE_CURRENT_SOURCE_DIR}/src/txn/txn_auto.c
${CMAKE_CURRENT_SOURCE_DIR}/src/txn/txn_chkpt.c
${CMAKE_CURRENT_SOURCE_DIR}/src/txn/txn_failchk.c
${CMAKE_CURRENT_SOURCE_DIR}/src/txn/txn_method.c
${CMAKE_CURRENT_SOURCE_DIR}/src/txn/txn_rec.c
${CMAKE_CURRENT_SOURCE_DIR}/src/txn/txn_recover.c
${CMAKE_CURRENT_SOURCE_DIR}/src/txn/txn_region.c
${CMAKE_CURRENT_SOURCE_DIR}/src/txn/txn_stat.c
${CMAKE_CURRENT_SOURCE_DIR}/src/txn/txn_util.c
${CMAKE_CURRENT_SOURCE_DIR}/src/xa/xa.c
${CMAKE_CURRENT_SOURCE_DIR}/src/xa/xa_map.c
${CMAKE_CURRENT_SOURCE_DIR}/src/common/zerofill.c

)

set(DB_CXX_SOURCES 
  ${CMAKE_CURRENT_SOURCE_DIR}/lang/cxx/cxx_channel.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/lang/cxx/cxx_db.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/lang/cxx/cxx_dbc.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/lang/cxx/cxx_dbstream.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/lang/cxx/cxx_dbt.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/lang/cxx/cxx_env.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/lang/cxx/cxx_except.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/lang/cxx/cxx_lock.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/lang/cxx/cxx_logc.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/lang/cxx/cxx_mpool.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/lang/cxx/cxx_multi.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/lang/cxx/cxx_rid.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/lang/cxx/cxx_seq.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/lang/cxx/cxx_site.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/lang/cxx/cxx_txn.cpp
  )


include_directories(
  ${CMAKE_CURRENT_SOURCE_DIR}
  ${CMAKE_CURRENT_SOURCE_DIR}/src
  )

# run configure if missing header files from configure
if (EXISTS	"${CMAKE_CURRENT_SOURCE_DIR}/db.h")
	else()	
		execute_process(
		  COMMAND ${CMAKE_CURRENT_SOURCE_DIR}/dist/configure --enable-cxx --disable-shared
		  WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
			)
endif()	


IF (${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
	add_library(db ${DB_SOURCES})
else()
	add_library(db ${DB_SOURCES} ${CMAKE_CURRENT_SOURCE_DIR}/src/mutex/mut_pthread.c)
endif()

add_library(db_cxx ${DB_CXX_SOURCES})



