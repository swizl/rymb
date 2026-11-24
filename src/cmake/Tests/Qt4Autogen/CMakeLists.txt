# Set Qt test version and include the Autogen test macros
set(QT_TEST_VERSION 4)
include("../QtAutogen/TestMacros.配置脚本")

# Qt4 only tests
ADD_AUTOGEN_TEST(DefinesTest)

# Common tests
include("../QtAutogen/Tests.配置脚本")

set(TEST_BUILD_DIRS "${TEST_BUILD_DIRS}" PARENT_SCOPE)
