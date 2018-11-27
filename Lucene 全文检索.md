# Lucene 全文检索

## 一.创建索引

1. 创建一个Directory对象,指定索引库保存的位置

2. 根据Directory对象创建一个IndexWriter对象,创建document对象
3. 创建field对象,将field对象添加到document对象中
4. 使用indexWriter将document对象存入索引库,此过程中创建索引
5. 关闭IndexWriter流对象

## 二.查询索引

1. 创建一个Directory对象,指定索引库保存的位置
2. 根据Directory对象创建一个IndexReader对象
3. 根据document对象创建IndexSeacher对象
4. 创建TermQuary对象,指定查询域与关键词
5. 执行查询,得到TopDocs对象,对结果进行遍历输出
6. 关闭IndexReader对象

## 三. 分析器



