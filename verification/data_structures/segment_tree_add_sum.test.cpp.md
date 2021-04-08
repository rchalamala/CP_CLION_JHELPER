---
data:
  _extendedDependsOn:
  - icon: ':question:'
    path: library/data_structures/segment_tree/segment_tree.hpp
    title: library/data_structures/segment_tree/segment_tree.hpp
  - icon: ':heavy_check_mark:'
    path: library/data_structures/segment_tree/segment_tree_functions/segment_tree_add.hpp
    title: library/data_structures/segment_tree/segment_tree_functions/segment_tree_add.hpp
  - icon: ':question:'
    path: library/general/speed.hpp
    title: library/general/speed.hpp
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    PROBLEM: https://judge.yosupo.jp/problem/point_add_range_sum
    links:
    - https://judge.yosupo.jp/problem/point_add_range_sum
  bundledCode: "#line 1 \"library/general/speed.hpp\"\n\n\n\n#include <iostream>\n\
    \ninline bool speed()\n{\n\tstd::cin.exceptions(std::cin.failbit);\n\treturn std::cin.tie(nullptr)\
    \ && std::ios_base::sync_with_stdio(false);\n}\n\n\n#line 2 \"verification/data_structures/segment_tree_add_sum.test.cpp\"\
    \n\n#define PROBLEM \"https://judge.yosupo.jp/problem/point_add_range_sum\"\n\n\
    #include <cstddef>\n#include <cstdint>\n#line 8 \"verification/data_structures/segment_tree_add_sum.test.cpp\"\
    \n#include <vector>\n\n#line 1 \"library/data_structures/segment_tree/segment_tree.hpp\"\
    \n\n\n\n#line 6 \"library/data_structures/segment_tree/segment_tree.hpp\"\n\n\
    template<class uF> class SegmentTree\n{\npublic:\n\tusing F = uF;\n\tusing Node\
    \ = typename F::Node;\n\tF f;\nprivate:\n\tconst std::size_t size;\n\tstd::vector<Node>\
    \ tree;\n\n\tvoid propagate(const std::size_t& i, const std::size_t& treeLeft,\
    \ const std::size_t& treeRight, const std::size_t& left, const std::size_t& right)\n\
    \t{\n\t\tif(treeLeft != treeRight)\n\t\t{ f.propagate_update(tree[i], tree[i <<\
    \ 1], tree[(i << 1) ^ 1], treeLeft, treeRight, left, right, size); }\n\t\telse\n\
    \t\t{ f.propagate_update(tree[i], tree[i], tree[i], treeLeft, treeRight, left,\
    \ right, size); }\n\t}\n\n\ttemplate<typename Iterable> void build(const std::size_t&\
    \ i, const std::size_t& left, const std::size_t& right, const Iterable& elements)\n\
    \t{\n\t\tif(left == right)\n\t\t{\n\t\t\ttree[i] = Node{elements[left]};\n\t\t\
    \treturn;\n\t\t}\n\t\tconst std::size_t midpoint = left + ((right - left) >> 1);\n\
    \t\tbuild(i << 1, left, midpoint, elements);\n\t\tbuild((i << 1) ^ 1, midpoint\
    \ + 1, right, elements);\n\t\ttree[i] = f.merge(tree[i << 1], tree[(i << 1) ^\
    \ 1]);\n\t}\n\n\ttemplate<typename... Arguments> void change(const std::size_t&\
    \ i, const std::size_t& treeLeft, const std::size_t& treeRight, const std::size_t&\
    \ left, const std::size_t& right, const Arguments& ... rest)\n\t{\n\t\tpropagate(i,\
    \ treeLeft, treeRight, left, right);\n\t\tif(left > treeRight || treeLeft > right)\n\
    \t\t{ return; }\n\t\tif(left <= treeLeft && treeRight <= right)\n\t\t{\n\t\t\t\
    f.change(tree[i], treeLeft, treeRight, left, right, size, rest...);\n\t\t\tpropagate(i,\
    \ treeLeft, treeRight, left, right);\n\t\t\treturn;\n\t\t}\n\t\tconst std::size_t\
    \ midpoint = treeLeft + ((treeRight - treeLeft) >> 1);\n\t\tchange(i << 1, treeLeft,\
    \ midpoint, left, right, rest...);\n\t\tchange((i << 1) ^ 1, midpoint + 1, treeRight,\
    \ left, right, rest...);\n\t\ttree[i] = f.merge(tree[i << 1], tree[(i << 1) ^\
    \ 1]);\n\t}\n\n\tNode range(const std::size_t& i, const std::size_t& treeLeft,\
    \ const std::size_t& treeRight, const std::size_t& left, const std::size_t& right)\n\
    \t{\n\t\tif(left > treeRight || treeLeft > right)\n\t\t{ return f.identity; }\n\
    \t\tpropagate(i, treeLeft, treeRight, left, right);\n\t\tif(left <= treeLeft &&\
    \ treeRight <= right)\n\t\t{ return tree[i]; }\n\t\tconst std::size_t midpoint\
    \ = treeLeft + ((treeRight - treeLeft) >> 1);\n\t\treturn f.merge(range(i << 1,\
    \ treeLeft, midpoint, left, right), range((i << 1) ^ 1, midpoint + 1, treeRight,\
    \ left, right));\n\t}\n\npublic:\n\texplicit SegmentTree(const std::size_t& uSize)\
    \ : size{uSize} { tree.assign(size << 2, Node{}); }\n\n\ttemplate<typename Iterable>\
    \ void build(const Iterable& uElements) { build(1, 0, size - 1, uElements); }\n\
    \n\ttemplate<typename... Arguments> void change(const std::size_t& left, const\
    \ std::size_t& right, const Arguments& ... rest) { change(1, 0, size - 1, left,\
    \ right, rest...); }\n\n\tauto range(const std::size_t& left, const std::size_t&\
    \ right) { return f.return_value(range(1, 0, size - 1, left, right)); }\n};\n\n\
    \n#line 1 \"library/data_structures/segment_tree/segment_tree_functions/segment_tree_add.hpp\"\
    \n\n\n\n#line 5 \"library/data_structures/segment_tree/segment_tree_functions/segment_tree_add.hpp\"\
    \n#include <type_traits>\n\ntemplate<typename uT, std::enable_if_t<std::is_arithmetic_v<uT>,\
    \ bool> = true> struct AddNode\n{\n\tusing T = uT;\n\n\tT value{}, delta{}, set{};\n\
    \tbool validSet{};\n\n\tAddNode(const T& uValue) : value{uValue} {}\n\n\tAddNode()\
    \ {}\n};\n\ntemplate<class uNode> struct Add\n{\n\tusing Node = uNode;\n\tusing\
    \ T = typename Node::T;\n\n\tNode identity{};\n\n\tvirtual T return_value(const\
    \ Node& element) { return element.value; }\n\n\tvirtual Node merge(const Node&\
    \ lhs, const Node& rhs) { return lhs.value + rhs.value; }\n\n\tvirtual void propagate_update(Node&\
    \ parent, Node& leftChild, Node& rightChild, const std::size_t& treeLeft, const\
    \ std::size_t& treeRight, const std::size_t& queryLeft, const std::size_t& queryRight,\
    \ const std::size_t& treeSize)\n\t{\n\t\tstd::size_t intervalLength{treeRight\
    \ - treeLeft + 1};\n\t\tif(parent.validSet)\n\t\t{\n\t\t\tif(intervalLength >\
    \ 1)\n\t\t\t{\n\t\t\t\tleftChild.set = rightChild.set = parent.set;\n\t\t\t\t\
    leftChild.validSet = rightChild.validSet = true;\n\t\t\t\tleftChild.delta = rightChild.delta\
    \ = 0;\n\t\t\t}\n\t\t\tparent.value = static_cast<T>(intervalLength) * parent.set;\n\
    \t\t\tparent.validSet = false;\n\t\t}\n\t\tif(parent.delta)\n\t\t{\n\t\t\tif(intervalLength\
    \ > 1)\n\t\t\t{\n\t\t\t\tleftChild.delta += parent.delta;\n\t\t\t\trightChild.delta\
    \ += parent.delta;\n\t\t\t}\n\t\t\tparent.value += static_cast<T>(intervalLength)\
    \ * parent.delta;\n\t\t\tparent.delta = 0;\n\t\t}\n\t}\n\n\tvirtual void change(Node&\
    \ element, const std::size_t& treeLeft, const std::size_t& treeRight, const std::size_t&\
    \ queryLeft, const std::size_t& queryRight, const std::size_t& treeSize, const\
    \ T& delta) { element.delta += delta; }\n\n\tvirtual void change(Node& element,\
    \ const std::size_t& treeLeft, const std::size_t& treeRight, const std::size_t&\
    \ queryLeft, const std::size_t& queryRight, const std::size_t& treeSize, const\
    \ T& set, const bool& notDelta)\n\t{\n\t\telement.delta = 0;\n\t\telement.set\
    \ = set;\n\t\telement.validSet = true;\n\t}\n};\n\n\n#line 12 \"verification/data_structures/segment_tree_add_sum.test.cpp\"\
    \n\nint main()\n{\n\tspeed();\n\tstd::size_t n;\n\tstd::int32_t q;\n\tstd::cin\
    \ >> n >> q;\n\tstd::vector<std::uint64_t> a(n);\n\tfor(auto& ai : a)\n\t{ std::cin\
    \ >> ai; }\n\tSegmentTree<Add<AddNode<std::uint64_t>>> segmentTree(n);\n\tsegmentTree.build(a);\n\
    \twhile(q--)\n\t{\n\t\tbool queryType;\n\t\tstd::cin >> queryType;\n\t\tif(queryType)\n\
    \t\t{\n\t\t\tstd::size_t l, r;\n\t\t\tstd::cin >> l >> r;\n\t\t\tstd::cout <<\
    \ segmentTree.range(l, r - 1) << '\\n';\n\t\t}\n\t\telse\n\t\t{\n\t\t\tstd::size_t\
    \ p;\n\t\t\tstd::uint64_t x;\n\t\t\tstd::cin >> p >> x;\n\t\t\tsegmentTree.change(p,\
    \ p, x);\n\t\t}\n\t}\n}\n"
  code: "#include \"../../library/general/speed.hpp\"\n\n#define PROBLEM \"https://judge.yosupo.jp/problem/point_add_range_sum\"\
    \n\n#include <cstddef>\n#include <cstdint>\n#include <iostream>\n#include <vector>\n\
    \n#include \"../../library/data_structures/segment_tree/segment_tree.hpp\"\n#include\
    \ \"../../library/data_structures/segment_tree/segment_tree_functions/segment_tree_add.hpp\"\
    \n\nint main()\n{\n\tspeed();\n\tstd::size_t n;\n\tstd::int32_t q;\n\tstd::cin\
    \ >> n >> q;\n\tstd::vector<std::uint64_t> a(n);\n\tfor(auto& ai : a)\n\t{ std::cin\
    \ >> ai; }\n\tSegmentTree<Add<AddNode<std::uint64_t>>> segmentTree(n);\n\tsegmentTree.build(a);\n\
    \twhile(q--)\n\t{\n\t\tbool queryType;\n\t\tstd::cin >> queryType;\n\t\tif(queryType)\n\
    \t\t{\n\t\t\tstd::size_t l, r;\n\t\t\tstd::cin >> l >> r;\n\t\t\tstd::cout <<\
    \ segmentTree.range(l, r - 1) << '\\n';\n\t\t}\n\t\telse\n\t\t{\n\t\t\tstd::size_t\
    \ p;\n\t\t\tstd::uint64_t x;\n\t\t\tstd::cin >> p >> x;\n\t\t\tsegmentTree.change(p,\
    \ p, x);\n\t\t}\n\t}\n}\n"
  dependsOn:
  - library/general/speed.hpp
  - library/data_structures/segment_tree/segment_tree.hpp
  - library/data_structures/segment_tree/segment_tree_functions/segment_tree_add.hpp
  isVerificationFile: true
  path: verification/data_structures/segment_tree_add_sum.test.cpp
  requiredBy: []
  timestamp: '2021-04-07 22:54:37-06:00'
  verificationStatus: TEST_ACCEPTED
  verifiedWith: []
documentation_of: verification/data_structures/segment_tree_add_sum.test.cpp
layout: document
redirect_from:
- /verify/verification/data_structures/segment_tree_add_sum.test.cpp
- /verify/verification/data_structures/segment_tree_add_sum.test.cpp.html
title: verification/data_structures/segment_tree_add_sum.test.cpp
---