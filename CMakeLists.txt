CMAKE_MINIMUM_REQUIRED(VERSION 2.8)

IF(NOT CMAKE_BUILD_TYPE)
  SET(CMAKE_BUILD_TYPE "RELEASE")
ENDIF()

project(vcash)

set(OPENSSL_VER "1.0.2j")
set(BERKELEY_DB_VER "6.1.29.NC")

IF (${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
	add_compile_options(-Wno-potentially-evaluated-expression -Wno-deprecated-declarations -Wno-inaccessible-base -Wno-unused-local-typedefs -Wno-logical-op-parentheses -Wno-shift-negative-value -Wno-array-bounds)
endif()

SET(SOURCES 
	${CMAKE_CURRENT_SOURCE_DIR}/src/account.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/accounting_entry.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/address.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/address_manager.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/alert.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/alert_manager.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/alert_unsigned.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/base58.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/big_number.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/blake256.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/block.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/block_index.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/block_index_disk.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/block_locator.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/block_merkle.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/chainblender.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/chainblender_broadcast.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/chainblender_join.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/chainblender_leave.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/chainblender_manager.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/chainblender_status.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/checkpoint_sync.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/checkpoint_sync_unsigned.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/checkpoints.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/configuration.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/crypter.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/database_stack.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/db.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/db_env.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/db_tx.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/db_tx_bdb.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/db_tx_ldb.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/db_wallet.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/ecdhe.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/file.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/filesystem.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/gateway.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/globals.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/hash.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/hc256.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/hd_configuration.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/hd_ecdsa.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/hd_keychain.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/http_transport.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/incentive.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/incentive_answer.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/incentive_collaterals.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/incentive_manager.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/incentive_question.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/incentive_sync.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/incentive_vote.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/inventory_vector.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/kernel.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/key.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/key_pool.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/key_public.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/key_reserved.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/key_store_basic.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/key_store_crypto.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/key_wallet.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/key_wallet_master.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/merkle_tree_partial.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/message.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/mining.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/mining_manager.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/nat_pmp.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/nat_pmp_client.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/point_in.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/point_out.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/reward.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/ripemd160.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/rpc_connection.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/rpc_json_parser.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/rpc_manager.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/rpc_server.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/rpc_transport.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/script.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/script_checker.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/script_checker_queue.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/secret.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/sha256.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/signature_cache.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/stack.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/stack_impl.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/status_manager.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/tcp_acceptor.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/tcp_connection.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/tcp_connection_manager.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/tcp_transport.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/transaction.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/transaction_bloom_filter.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/transaction_in.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/transaction_index.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/transaction_merkle.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/transaction_out.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/transaction_pool.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/transaction_position.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/transaction_wallet.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/upnp_client.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/utility.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/wallet.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/wallet_manager.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/whirlpool.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/zerotime.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/zerotime_answer.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/zerotime_lock.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/zerotime_manager.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/zerotime_question.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/zerotime_vote.cpp
	)

set(DATABASE_SOURCES 
	${CMAKE_CURRENT_SOURCE_DIR}/database/src/block.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/database/src/broadcast_operation.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/database/src/compression.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/database/src/ecdhe.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/database/src/entry.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/database/src/find_operation.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/database/src/hc256.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/database/src/key_pool.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/database/src/message.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/database/src/node.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/database/src/node_impl.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/database/src/operation.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/database/src/operation_queue.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/database/src/ping_operation.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/database/src/query.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/database/src/routing_table.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/database/src/rpc.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/database/src/slot.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/database/src/stack.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/database/src/stack_impl.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/database/src/storage.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/database/src/store_operation.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/database/src/udp_handler.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/database/src/udp_multiplexor.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/database/src/whirlpool.cpp
	)

IF (${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
	set(OPENSSL_ROOT_DIR "/usr/local/Cellar/openssl/${OPENSSL_VER}/")
endif()

find_package(OpenSSL)
if (OPENSSL_FOUND)
  message(STATUS "Found OpenSSL")
endif()  

find_package( Boost COMPONENTS system )
link_directories ( ${Boost_LIBRARY_DIRS} )

include_directories(
	${CMAKE_CURRENT_SOURCE_DIR}/include
	${CMAKE_CURRENT_SOURCE_DIR}/database/include
	${Boost_INCLUDE_DIRS}
  ${OPENSSL_INCLUDE_DIR}
	${CMAKE_CURRENT_SOURCE_DIR}/deps/db-${BERKELEY_DB_VER}
	${CMAKE_CURRENT_SOURCE_DIR}/deps/leveldb/leveldb/include
  )

add_definitions("-D_FILE_OFFSET_BITS=64" "-DBOOST_NO_CXX11_NUMERIC_LIMITS")

add_library(coin ${SOURCES})
set_property(TARGET coin PROPERTY CXX_STANDARD 11)

add_library(database ${DATABASE_SOURCES})
set_property(TARGET database PROPERTY CXX_STANDARD 11)

add_subdirectory(deps/db-${BERKELEY_DB_VER})
add_subdirectory(deps/leveldb)

add_executable(vcashd ${CMAKE_CURRENT_SOURCE_DIR}/test/main.cpp)
set_property(TARGET vcashd PROPERTY CXX_STANDARD 11)
target_link_libraries(vcashd coin database db_cxx db leveldb ${OPENSSL_LIBRARIES} ${Boost_LIBRARIES} pthread)

# Build app if wxVcashGUI subdirectory exists
if (EXISTS	"${CMAKE_CURRENT_SOURCE_DIR}/wxVcashGUI")
	add_subdirectory(wxVcashGUI)
endif()	