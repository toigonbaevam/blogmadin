.. _role:

================
开发建议
================

#. **代码路径**

   .. attention::

      重要！！ 你所有的代码都应放在 ``custom_`` 开头的文件夹下

#. **导入model**

    你应该从 ``app.app_models`` 中导入，而不是从 ``app.models`` 中，如:: 

        from app.app_models.content_model import Article

#. **Config命名**

    如果你需要用到config，建议给config取一个本地化语言的名字，而不是英语名。 
    你可以用一个dict保存英语名与本地化名，如:: 

        config_name={

            'top_menu':'顶部导航栏'
        }

        # 使用时

        create_config( name=config_name['top_menu'], v2_config='' )

        config = get_config( name=config_name['top_menu'] )

#. **如何获取Config**

    获取config时，你应该从 ``config.v2_real_config`` 中读取配置，``config.v2_config`` 中的配置是未进handler处理的:: 

        from ast import literal_eval
        from app.db_manager.config_manager import get_config_by_name
        from app.consts import app_config_context

        iconbar_config=get_config_by_name(app_config_context['v2_iconbar_config'])

        print(iconbar.v2_real_config)


#. **dispatch_uid**

    如果你要使用绑定model的信号，需要注意DeerU预定了 "model名_信号名" 格式的 dispatch_uid ，如："article_pre_save"，"article_post_save"。
    建议在dispatch_uid前加上你的昵称或包名，防止冲突。
