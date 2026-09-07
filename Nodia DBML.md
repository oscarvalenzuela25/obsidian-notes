```
Table users [headercolor: #175e7a] {

    id bigint [ pk, increment, not null ]

    name varchar(255)

    email text [ not null, unique ]

    image_url text

    is_active boolean [ not null, default: true ]

    created_at timestamp [ not null ]

    updated_at timestamp [ not null ]

}

  

Table roles [headercolor: #175e7a] {

    id bigint [ pk, increment, not null ]

    key text [ not null, unique ]

    is_active boolean [ not null, default: true ]

    created_at timestamp [ not null ]

    updated_at timestamp [ not null ]

}

  

Table actions [headercolor: #175e7a] {

    id bigint [ pk, increment, not null ]

    module_id bigint

    key text [ not null, unique ]

    description text

    is_active boolean [ not null, default: true ]

    created_at timestamp [ not null ]

    updated_at timestamp [ not null ]

}

  

Table modules [headercolor: #175e7a] {

    id bigint [ pk, increment, not null ]

    key text [ not null, unique ]

    type text [ not null ]

    parent_id bigint

    is_active boolean [ not null, default: true ]

    created_at timestamp [ not null ]

    updated_at timestamp [ not null ]

}

  

Table role_actions [headercolor: #175e7a] {

    id bigint [ pk, increment, not null ]

    role_id bigint [ not null ]

    action_id bigint [ not null ]

    is_active boolean [ not null, default: true ]

    created_at timestamp [ not null ]

    updated_at timestamp [ not null ]

  

    indexes {

        (role_id, action_id) [ name: 'uq_role_action', unique ]

    }

}

  

Table user_roles [headercolor: #175e7a] {

    id bigint [ pk, increment, not null ]

    user_id bigint [ not null ]

    role_id bigint [ not null ]

    is_active boolean [ not null, default: true ]

    created_at timestamp [ not null ]

    updated_at timestamp [ not null ]

  

    indexes {

        (user_id, role_id) [ name: 'uq_user_role', unique ]

    }

}

Table translations [headercolor: #175e7a] {
	id bigint [ pk, increment, not null ]
	key varchar(255) [ not null ]
	locale varchar(10) [ not null ]
	value text [ not null ]
	created_at timestamp [ not null ]
	updated_at timestamp [ not null ]

	indexes {
		(key, locale) [ name: 'uq_translation_key_locale', unique ]
		(locale, key) [ name: 'idx_translation_locale_key' ]
	}
}

  

Ref fk_actions_module {

    actions.module_id > modules.id [ delete: no action, update: no action ]

}

  

Ref fk_modules_parent {

    modules.parent_id > modules.id [ delete: no action, update: no action ]

}

  

Ref fk_role_actions_role {

    role_actions.role_id > roles.id [ delete: no action, update: no action ]

}

  

Ref fk_role_actions_action {

    role_actions.action_id > actions.id [ delete: no action, update: no action ]

}

  

Ref fk_user_roles_user {

    user_roles.user_id > users.id [ delete: no action, update: no action ]

}

  

Ref fk_user_roles_role {

    user_roles.role_id > roles.id [ delete: no action, update: no action ]

}
```