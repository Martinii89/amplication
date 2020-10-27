# Migration `20201025114636-new-data-types`

This migration has been generated by Yuval Hazaz at 10/25/2020, 1:46:37 PM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
Begin;
CREATE TYPE "public"."EnumDataType_new" AS ENUM ('SingleLineText', 'MultiLineText', 'Email', 'WholeNumber', 'DateTime', 'DecimalNumber', 'Lookup', 'MultiSelectOptionSet', 'OptionSet', 'Boolean', 'GeographicLocation', 'Id', 'CreatedAt', 'UpdatedAt', 'Roles', 'Username', 'Password');
ALTER TABLE "public"."EntityField" ALTER COLUMN "dataType" TYPE "EnumDataType_new" USING ("dataType"::text::"EnumDataType_new");
ALTER TYPE "EnumDataType" RENAME TO "EnumDataType_old";
ALTER TYPE "EnumDataType_new" RENAME TO "EnumDataType";
DROP TYPE "EnumDataType_old";
Commit
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration 20201020190047-deployment-status-query..20201025114636-new-data-types
--- datamodel.dml
+++ datamodel.dml
@@ -1,7 +1,7 @@
 datasource db {
   provider = "postgresql"
-  url = "***"
+  url = "***"
 }
 generator client {
   provider = "prisma-client-js"
@@ -239,12 +239,15 @@
   Lookup
   MultiSelectOptionSet
   OptionSet
   Boolean
-  GeographicAddress
+  GeographicLocation
   Id
   CreatedAt
   UpdatedAt
+  Roles
+  Username
+  Password
 }
 model Block {
   id            String         @id @default(cuid())
```

