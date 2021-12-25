# DDD实践学习笔记

## 1 DDD片面了解与疑问

DDD与瀑布、RUP、敏捷有什么差异？如何融合？
DDD是设计方法思路，那需求分析呢？如何匹配？还是没有需求分析，直接设计？
有的微服务模式只直接读写访问自己独有的DB，跨微服务的一致性用消息队列来确保最终一致性。
有的微服务模式中微服务只能通过消息队列机制写共享DB。

究竟用哪种模式，可能跟开发团队组织结构有关。

DDD最大的特点是用面向对象方法刻画业务本身，对业务建模、软件设计、编码实现。
没有明确提及RUP中的Actor和跨泳道业务流程。优点：业务核心对象的本质操作稳定性和复用性很高，即使为了监督等增加非必要业务操作或不同的组织结构岗位分工，核心业务对象和本质操作也不变。为便于技术人员理解，以软件开发过程为例来说明应用软件针对的业务，业务流程变化会改变主要工作任务的先后顺序和负责角色，但各项主要工作任务却基本没有变化。

例1：最早先的瀑布白盒测试中分割出单元测试，现代软件工程中执行人由测试工程师改为软件工程师，流程顺序提前到代码提交中央代码库之前。

例2：传统瀑布测试文档中的功能测试通过条件，分割出UserStory的验收条件。编写人由测试工程师改为产品经理/需求分析师，流程顺序提前到需求阶段。

更适用于对客观世界中事物的建模，适用于应用软件开发。不适用于基础软件或事务简单结构复杂的软件研发，如：数据库、操作系统、AI模型。

简单的说，适用于软件人员为非软件人员设计开发业务系统应用软件，而不适用软件人员为软件人员设计开发类库、框架或中间件等。

微服务架构下，统一的前端调用多个微服务实现业务操作。
而微服务的划分如按DDD方法是按限界上下文划分，是在聚合根这种业务对象之间划分。而各个聚合根之间均为天热松耦合。保障了微服务划分的高内聚松耦合，减少了微服务之间互相调用。

限界上下文内跨聚合根、跨对象的操作建模成服务。跨限界上下文的操作也应建模成应用内的顶级服务，或是简单业务编排由前端/BFF（Backend For Frontend)编码实现。

备注：本文中UML图采用[PlantUML代码](DDD_LearningNote.puml)在[PlantUML demo server](http://www.plantuml.com/plantuml/)生成

## 2 学习计划

根据先总体后局部的学习方法，学习计划分以下几步

### 2.1 理论学习：读书

### 2.2 实践学习：看代码

### 2.3 总结

## 3 C# 实现方式

参考微软提供的示例代码 [eShopOnWeb](https://github.com/dotnet-architecture/eShopOnWeb) & [eShopOnContainers](https://github.com/dotnet/eShopOnContainers)



![.NET示例代码中分层架构图](//www.plantuml.com/plantuml/png/SoWkIImgAStDKN1nST7pSmtHSonApiWiIKqkAIrAzKciJ2qAoqmjvof8JCvEJ4zL24zDuihBBqbLACfCpoYn0kbwicFjyrajZWK5EPd9YIMP-NbFDpR1rIC9E-SNfMBNwvAVcvY9eiqpBwqeiRYag1Je35owKDM0T0CTfw2dPuTXAQfAR4fWMj4jTaZDIm463W00)



![.NET示例代码中领域模型层示意类图](//www.plantuml.com/plantuml/png/ZLFBRjim4BphA_QOj7P-e8QHs0uA0K4SE4uBz58mubfPL285SjL2TVFl5IcASYiBS4xSnynEPgnRoy9mNHQmsMnk7k_tDnjT2b8Fea6pBeIrNmX_9PbxmTP8DCS4sh-Fi5XKHbTek5akmR8XbSEgRb6fX6EE_0agGpy58rZaztEWJJlSKudRmy4YT-okTo7yJag3riBp6rLx7Qefx1mUoFB2tqWPooLyr_qxaASx57AhYcQjYm8p9grEz-FJ1aBVkBhkqA4AFhnsFioYHdkgSJRIGewsPvAOKIaAs6iMHSl_dYHNrv3UvRcXN33kjERatnBcGKuIamhSPzDQYvPPvsxk5r72yBumlIZpHH4_6SekZOqKUynqL8FwwExG6Mllt9j5GNKlQEPlkT8w5_qwV9ZFJx9C4l5gsOYCOIKitYicRevJibC9BS-m28i_qVXHDvu8aOJmUtA3GcfLDFsdyym6aIU6wvPs4YSOfs2wLcocaD-eMck9mVCWBphUrs7PUdcp7fiHDx6mJi8mwex6-dTtPaZ01H3Oa-YIxuwp3TwD1oCRIV7fMYed_kidesMTyQCeSMg3CguDlXWAreolHvVEZ9mGyWgY1TLmS-Z5A_uBRr5e3Y93I3tH3YjjYRM9lyQzi3yMVhQ4pyYh9fLVYT_SQNjd6vLrbwMZ-vy3uey-kKKbwx98_W80)



![.NET示例代码中Infrastructure层实现示意类图](//www.plantuml.com/plantuml/png/XP51IyGm48Nl-HK3NbPq-mCMNLRRHNfHaA97YSaKmwQ991EqgF_TjgnDR0jxASthU--RJdQUkAFGQ2YA8hlVLrbfQiSzkI0eECmrz_v9uGTJXj3LN22KDxuruX7VhLTaNGjNrVQB0G1SGCNzeJl27T9jMyh1kUgYeEGbvDm8r9gJigQo1pH0m_CQ9DOyQ3fdFoddmKbqaVEFCNmRES-Atah2ngV0latqyyE-ZYtZi6TGlEQsetqIlCY_roCZJQoYRxJ5xkKXf_9Yn-cTzPZf6c2z_jxEBs4pauuxOelvz0StoId6KWsoR86PDAUkYSfsQ6HeDFi5)



```C#
    public class OrderConfiguration : IEntityTypeConfiguration<Order>
    {
        public void Configure(EntityTypeBuilder<Order> builder)
        {
			//---------------------------------------------
			//这段藏在Migeration目录代码中，转移到这里提高可读性
			b.Property<int>("Id")
	             .ValueGeneratedOnAdd()
                  .HasColumnType("int")
                  .UseIdentityColumn();
             b.Property<string>("BuyerId")
                  .HasColumnType("nvarchar(max)");
             b.Property<DateTimeOffset>("OrderDate")
                  .HasColumnType("datetimeoffset");
             b.HasKey("Id");
             b.ToTable("Orders");
			//---------------------------------------------
			
			var navigation = builder.Metadata.FindNavigation(nameof(Order.OrderItems));
            navigation.SetPropertyAccessMode(PropertyAccessMode.Field);
            builder.OwnsOne(o => o.ShipToAddress, a =>
            {
                a.WithOwner();
                a.Property(a => a.ZipCode)
                    .HasMaxLength(18)
                    .IsRequired();
                a.Property(a => a.Street)
                    .HasMaxLength(180)
                    .IsRequired();
                a.Property(a => a.State)
                    .HasMaxLength(60);
                a.Property(a => a.Country)
                    .HasMaxLength(90)
                    .IsRequired();
                a.Property(a => a.City)
                    .HasMaxLength(100)
                    .IsRequired();
            });
        }
    }


    public class CatalogContext : DbContext
    {
        public CatalogContext(DbContextOptions<CatalogContext> options) : base(options)
        {
        }
        public DbSet<Basket> Baskets { get; set; }
        public DbSet<CatalogItem> CatalogItems { get; set; }
        public DbSet<CatalogBrand> CatalogBrands { get; set; }
        public DbSet<CatalogType> CatalogTypes { get; set; }
        public DbSet<Order> Orders { get; set; }
        public DbSet<OrderItem> OrderItems { get; set; }
        public DbSet<BasketItem> BasketItems { get; set; }
        protected override void OnModelCreating(ModelBuilder builder)
        {
            base.OnModelCreating(builder);

			//Applies config from all IEntityTypeConfiguration<TEntity> instance defined in assembly
            builder.ApplyConfigurationsFromAssembly(Assembly.GetExecutingAssembly());
            
            /*或者如下方所示意，手工调用每个聚合根(AggrigateRoot)的配置类
            OrderConfiguration.Configure(builder);
            BasketConfiguration.Configure(builder);
            */
        }
    }

```



## 4 Java实现方式