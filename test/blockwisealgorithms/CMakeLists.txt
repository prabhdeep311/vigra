VIGRA_CONFIGURE_THREADING()
if(NOT THREADING_FOUND)
    MESSAGE(STATUS "** WARNING: Your compiler does not support C++ threading.")
    MESSAGE(STATUS "**          test_blockwiselabeling will not be executed on this platform.")
    if(NOT WITH_BOOST_THREAD)
        MESSAGE(STATUS "**          Try to run cmake with '-DWITH_BOOST_THREAD=1' to use boost threading.")
    endif()
    
else()
    SET(MULTIARRAY_CHUNKED_LIBRARIES ${THREADING_LIBRARIES})
    VIGRA_ADD_TEST(test_blockwiselabeling test_labeling.cxx LIBRARIES ${MULTIARRAY_CHUNKED_LIBRARIES})
    VIGRA_ADD_TEST(test_blockwisewatersheds test_watersheds.cxx LIBRARIES ${MULTIARRAY_CHUNKED_LIBRARIES})
    VIGRA_ADD_TEST(test_blockwiseconvolution test_convolution.cxx LIBRARIES ${MULTIARRAY_CHUNKED_LIBRARIES})
endif()