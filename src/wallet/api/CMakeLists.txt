add_library(wallet_api
  wallet.cpp
  wallet_manager.cpp
  transaction_info.cpp
  transaction_history.cpp
  pending_transaction.cpp
  utils.cpp
  address_book.cpp
  subaddress.cpp
  subaddress_account.cpp
  unsigned_transaction.cpp)

target_link_libraries(wallet_api
  PUBLIC
    wallet
    cryptonote_core
    mnemonics
    lmdb
    Boost::chrono
    Boost::serialization
    Boost::filesystem
    Boost::thread
    Boost::regex
  PRIVATE
    extra)

set_property(TARGET wallet_api PROPERTY EXCLUDE_FROM_ALL TRUE)

if(IOS)
    set(lib_folder lib-${ARCH})
else()
    set(lib_folder lib)
endif()

install(FILES ${wallet_api_headers}
    DESTINATION include/wallet/api)
