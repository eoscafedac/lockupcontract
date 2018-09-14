# lockupcontract

adding lock, unlock method and table to the original eosio.token contract.
Currently support all or nothing lockup. If a user name in the lockup table, he or she can transfer nothing.
Next phase, progressive lockup will be provided.

# Usage
lock : Lock transfefr token to others
parameter : 
- user : EOS account name
- period : lockup period, unit is week.

unlock : unlock transfer token to others
parameter : 
- user : EOS account name

# Table structure
         struct lockup_list {
            account_name user;
            uint64_t allow_amount;
            uint32_t lockup_period;
            uint32_t set_time;
            
            uint64_t primary_key()const {return user;}
            EOSLIB_SERIALIZE(lockup_list,(user)(allow_amount)(lockup_period)(set_time))
         };
allow_amount and set_time are future usage. The reason why I added unused ones here is to preserve contract table data on upgrading.

user : EOS account name
allow_amount : If progressive lock is enabled, this field indicates how much amount currently user transfer.
allow_amount can be calculated by update_lockup_table function will be provided in near future.
lockup_period : ending time of lock up.
set_time : lock transaction execution time.


@copyright EOS CAFE DAC
